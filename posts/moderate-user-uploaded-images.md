---
title: "How to moderate user-uploaded images"
date: 2026-10-26
description: "Check avatars, listing photos and attachments before they go live. Send base64 images to the Supervisor API, understand how images are billed, and handle OCR text and errors."
---

# How to moderate user-uploaded images

**Bottom line:** base64 encode the upload, send it in the `image` field of the same `/moderate` endpoint you use for text, and act on the labels. Images and text go in separate requests, and images are billed by file size at a flat rate. This guide uses Python.

## The problem

Anything users can upload will eventually be abused: avatars, listing photos, profile banners, screenshots in support tickets. Human review of every upload does not scale, and filename checks do not tell you what is in the picture. You also need to catch text inside images, because screenshots of abuse and scam messages are a common way around text filters.

## 1. Set up

Sign up at [supervisor.gg](https://supervisor.gg), create a key under **Dashboard > API Keys** (`sk_prod_...`) and install the SDK:

```bash
pip install "git+https://github.com/Phosphor-gg/supervisor-sdk-python.git"
```

Image and video moderation are included with Premium.

## 2. Send an image

```python
import base64
import os
from pathlib import Path
from supervisor import SyncSupervisorClient, ModerationModel

client = SyncSupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"])

def check_image(path: str):
    image_b64 = base64.b64encode(Path(path).read_bytes()).decode()
    return client.moderate(image=image_b64, model=ModerationModel.SENTINEL)

result = check_image("upload.jpg")
print(result.flagged, result.labels)
```

The same request over HTTP:

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "image": "<base64-encoded image data>",
    "model": "sentinel"
  }'
```

The response has the same shape as for text: `flagged`, `labels` and `model_version`.

Rules to remember:

- Send text and images in separate requests. If an upload has a caption, moderate the caption as text.
- The SDK prepares the image before upload. In Python it strips a `data:` prefix, downsizes to at most 1280 pixels on the longest edge, flattens transparency and re-encodes as JPEG, if Pillow is installed. Without Pillow, the image is sent unchanged.

## 3. Understand the cost

Images are billed at a flat rate of about £0.0014 per KB of image data (the Observer rate), whichever model you pick. If OCR finds readable text in the image, that text is billed in addition at the model's text rate, so you only pay text prices when text is actually found.

From the docs' own examples: a 100 KB image with no readable text costs about £0.14 on any model. Cached results are free: repeating an identical request (or a near-identical image) within the cache window consumes no credits.

## 4. Decide what to do with the labels

Choose labels to match your rules with `enabled_labels`. For uploads, the common ones are `sexual`, `sexual/explicit`, `sexual/unlawful`, `violence`, `self-harm`, `hate` and `illegal`:

```python
from supervisor import ModerationLabel

BLOCK = [
    ModerationLabel.SEXUAL_EXPLICIT,
    ModerationLabel.SEXUAL_UNLAWFUL,
    ModerationLabel.VIOLENCE,
    ModerationLabel.HATE,
    ModerationLabel.ILLEGAL,
]

def review_upload(path: str) -> str:
    result = client.moderate(
        image=base64.b64encode(Path(path).read_bytes()).decode(),
        enabled_labels=BLOCK,
    )
    return "reject" if result.flagged else "accept"
```

## 5. Handle errors and credits

```python
from supervisor import SupervisorError

try:
    verdict = review_upload("upload.jpg")
except SupervisorError as e:
    if e.status_code == 402:
        notify_admin("moderation credits exhausted")
    verdict = "hold"  # keep the upload private until it has been checked
```

`402 Payment Required` means your credits have run out until the monthly reset or an upgrade. Holding uploads on any error stops an outage from publishing unchecked images. `notify_admin` is your own function.

## 6. When to check

- **Before it is visible to others.** Save the upload as private, moderate, then publish. This is the only point at which a block means anything.
- **Avatars and banners** deserve the check because they appear everywhere.
- **Do not re-check unchanged files.** Store the verdict against the file hash.

## Summary

- Base64 image in the `image` field, separate from text.
- Billed at about £0.0014 per KB, plus OCR text at the model rate.
- Hold uploads until checked, and treat `402` as a planned state.

Videos work similarly: see [how to moderate user-uploaded videos](/blog/moderate-user-uploaded-videos). Read the [API reference](/docs/integrations/api), try an image in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
