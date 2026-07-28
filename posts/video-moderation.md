---
title: "Video moderation is live"
description: "Send a clip, get back the moments that matter. Supervisor decodes video on the GPU, picks the frames where the picture actually changes, and tells you the timestamp of anything it flags."
date: 2026-07-28
---

# Video moderation is live

Supervisor now moderates video. Send a clip to the API or post one in a Discord server the bot is watching, and you get back the same labels you already get for text and images, with a timestamp for each frame that triggered.

It is included in the plan, which as of today is [the only plan](/blog/one-plan-everything-included).

## Using it

```bash
curl -X POST https://supervisor.gg/api/moderation/user/video \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "video": "BASE64_ENCODED_VIDEO", "model": "arbiter" }'
```

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

The SDKs wrap it in one call, and check the size limit locally so an oversized clip fails before it is uploaded rather than after:

```python
result = client.moderate_video("clip.mp4")
```

```javascript
const result = await client.moderateVideo(videoBytes);
```

In Discord, it is a toggle in the dashboard next to image moderation. It is off by default, so turning it on is a deliberate choice. Once it is on, video attachments in moderated channels go through the same rules as everything else.

## Timestamps, not just a verdict

`frames` carries a `timestamp_ms` for every frame analysed, so you can jump to the moment that triggered rather than being told "this video is bad" and having to watch it yourself. The top level `labels` is the union across every frame.

This is the part that makes video moderation usable for an actual moderator. A verdict on a sixty second clip is a starting point. A verdict plus "2.1 seconds in" is an action.

## Why we do not look at every frame

A sixty second clip at 30fps is 1,800 frames, and almost all of them are the previous frame again. Analysing all of them would be slow and would cost you a fortune for no extra signal.

Instead Supervisor pulls a candidate frame every 500ms, then throws away the ones that are not new. Two frames count as the same shot only when **both** of these hold:

- their difference hashes are within 6 bits of each other (out of 64), and
- every cell of a 4x4 mean colour grid is within 24 of the other frame's (out of 255)

Both conditions are needed, and that is not obvious. A difference hash reads luminance gradients, so two flat scenes in completely different colours hash identically and a cut between them looks like no cut at all. Colour alone goes wrong the other way, merging genuinely different scenes that happen to share a palette. Requiring both catches what either misses on its own. We found this the hard way, on a test clip where a red scene and a blue scene were being collapsed into one.

What survives is capped at 20 frames, spread across the timeline rather than taken from the start, so a long clip is not analysed only at its opening.

## Decoding on the GPU

H.264 and HEVC decode on the GPU through NVDEC, which is dedicated silicon for exactly this and leaves the GPU's compute units free for the models. VP9 and AV1 have no hardware support on our cards, so they fall back to software decode and are slower.

The response tells you which one ran, in the `decoder` field. That is there deliberately: a silent fallback to CPU decode is the kind of thing that quietly costs you throughput for months, so we made it visible rather than internal.

## The limits

| Limit | Value |
| --- | --- |
| File size | 10 MB |
| Duration | 60 seconds |
| Frames analysed | 20 maximum |

All three are enforced on our side and mirrored in the SDKs. 10 MB is Discord's default attachment limit, so bot coverage is close to total.

These are deliberately conservative for a first release. If they turn out to be the wrong shape for what people actually send, we would rather raise them later than launch with limits we cannot serve.

## What it costs

Video frames are billed by byte like images, but at **a quarter of the image rate**, and a clip with more than one frame also gets the **50% batch discount**, because the whole batch goes through the models in one pass rather than one pass each.

Together that makes a megabyte of extracted frames cost about **£0.17**, where the same bytes sent as images would cost about £1.40. Eight times cheaper per byte, before you count the frames dedup threw away.

Frames are also extracted at 720px rather than the 1,280px used for a standalone image, so there are fewer bytes to bill in the first place. The vision model sees 224px either way, so past roughly 720px the extra pixels only buy legibility for text inside the frame, and they cost money in a straight line.

## Try it

Video moderation is live now for everyone on the plan. If you want to see the models work before signing up for anything, the [demo](https://supervisor.gg/demo) takes text with no account, or [add the bot](https://supervisor.gg/discord-bot) and turn the toggle on.
