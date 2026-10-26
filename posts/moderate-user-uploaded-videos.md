---
title: "How to moderate user-uploaded videos"
date: 2026-10-26
description: "Moderate short video uploads with one API call: the 10 MB and 60 second limits, per-frame timestamps, how video is billed, and SDK examples in Python, JavaScript and Go."
---

# How to moderate user-uploaded videos

**Bottom line:** send the whole clip to `POST /api/moderation/user/video` as base64. Supervisor picks the frames where the picture changes, moderates those, and returns a verdict plus a timestamp for each frame it analysed. Clips are limited to 10 MB and 60 seconds.

## The problem

You cannot watch every upload, and you cannot moderate 1,800 frames for every minute of footage either. A useful video check has to choose frames sensibly, tell you where in the clip the problem is, and not cost more than the video is worth.

## What the endpoint does

Per the API reference, Supervisor decodes the clip, picks out the frames where the picture changes rather than every frame, and moderates those through the same pipeline as images. A sixty second clip costs a handful of frames, not hundreds.

| Limit | Value |
| --- | --- |
| File size | 10 MB |
| Duration | 60 seconds |
| Frames analysed | 20 maximum |

All three are enforced server-side. The SDKs also check the size limit locally, so an oversized clip fails before it is uploaded. Video moderation requires the video-moderation feature, which Premium includes.

## Raw request

```bash
curl -X POST https://supervisor.gg/api/moderation/user/video \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "video": "BASE64_ENCODED_VIDEO",
    "model": "arbiter"
  }'
```

An example response:

```json
{
  "flagged": true,
  "labels": ["violence"],
  "frames": [
    { "timestamp_ms": 0, "flagged": false, "labels": [] },
    { "timestamp_ms": 2133, "flagged": true, "labels": ["violence"] }
  ],
  "frames_analysed": 2,
  "duration_secs": 6.4,
  "codec": "h264",
  "decoder": "nvdec"
}
```

Top level `labels` is the union across every frame. `frames` has a `timestamp_ms` for each analysed frame, so a moderator can jump straight to the flagged moment. `codec` and `decoder` report what was detected and which decoder ran. H.264 and HEVC decode on the GPU; VP9 and AV1 fall back to software decode and are slower.

## Python

```python
import os
from supervisor import SyncSupervisorClient, ModerationModel, ValidationError

client = SyncSupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"])

try:
    result = client.moderate_video("clip.mp4", model=ModerationModel.ARBITER)
except ValidationError as e:
    print("rejected before upload:", e)  # for example, the file is over 10 MB
else:
    if result.flagged:
        for frame in result.frames:
            if frame.flagged:
                print(f"{frame.timestamp_ms} ms: {frame.labels}")
```

`moderate_video(path, model=None, enabled_labels=None)` takes a file path and returns a `VideoModerationResponse`.

## JavaScript

```typescript
import { readFile } from "node:fs/promises";
import { SupervisorClient } from "supervisor-sdk";

const client = new SupervisorClient({ apiKey: process.env.SUPERVISOR_API_KEY! });

const videoBytes = await readFile("clip.mp4");
const result = await client.moderateVideo(videoBytes);

for (const frame of result.frames) {
  if (frame.flagged) console.log(frame.timestamp_ms, frame.labels);
}
```

`moderateVideo` accepts bytes, a Blob or a base64 string, and rejects if the clip is over the limit.

## Go

```go
data, err := os.ReadFile("clip.mp4")
if err != nil {
	return err
}
res, err := client.ModerateVideo(ctx, data,
	supervisor.WithVideoModel(supervisor.ModelArbiter),
	supervisor.WithVideoLabels(supervisor.LabelViolence, supervisor.LabelSexualExp),
)
if err != nil {
	return err
}
for _, f := range res.Frames {
	if f.Flagged {
		fmt.Println(f.TimestampMs, f.Labels)
	}
}
```

## Cost

Video frames are billed at a quarter of the image rate, and are extracted at a smaller size than a standalone image, so a full 20 frame clip costs far less than 20 images. A clip goes through as one batch, so the 50% batch discount applies to the frames too. Check the pricing for the exact figures rather than relying on rules of thumb.

## Pattern for an upload flow

1. Accept the upload and store it as private.
2. If it is over 10 MB or 60 seconds, tell the user it is too long for the moderated path, or trim it.
3. Call the video endpoint.
4. If `flagged`, route to a moderator with the flagged timestamps. Otherwise publish.
5. On `402`, which means credits have run out until the monthly reset or an upgrade, keep clips private and alert someone.

Also scan the thumbnail and title: they are an image and text, and go through the normal [image](/blog/moderate-user-uploaded-images) and text endpoints.

## Summary

- One call, whole clip, base64, up to 10 MB and 60 seconds.
- Verdict per frame with timestamps, up to 20 frames.
- Billed per frame at a fraction of the image rate.
- Hold clips until checked.

Read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg) and get an API key. There is a background post on [video moderation](/blog/video-moderation) too.
