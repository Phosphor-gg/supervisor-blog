---
title: "Best image moderation APIs in 2026"
date: 2026-10-26
description: "Seven image moderation APIs compared from their own docs: OpenAI, Azure, AWS Rekognition, Hive, Sightengine, Moderation API and Supervisor, with size limits, formats and honest best-for notes."
---

# Best image moderation APIs in 2026

**Bottom line:** for free image screening in an LLM product, start with OpenAI. For taxonomies with many visual classes, look at Sightengine, Hive and AWS Rekognition. Azure suits teams already on Azure that want severity levels. **Supervisor**, our own product, is best when images are one of several media types on a community or platform and you also want the text and video handled by the same API, with the same labels, and the option of a Discord bot.

Everything here was read from vendor docs on 26 October 2026. We have not tested accuracy, so this is a comparison of what each product says it does, its limits and its price shape.

## At a glance

| | Image formats and size | Output | Pricing shape |
| --- | --- | --- | --- |
| Supervisor | Base64 image through `/moderate` | Labels and `flagged` | Billed per byte, same plan as text |
| OpenAI | Up to 20 MB | Categories and scores | Free |
| Azure | 4 MB, 50 to 7,200 px, JPEG PNG GIF BMP TIFF WEBP | Severity 0, 2, 4, 6 per category | USD per 1,000 images |
| AWS Rekognition | PNG or JPEG, 5 MB bytes or 15 MB in S3 | Hierarchical labels with confidence | USD per image |
| Hive | GIF JPG PNG WEBP | Class confidence scores | Per request list rate, or sales |
| Sightengine | 12 MB on all plans shown | Score per class | Monthly plans from $29 |
| Moderation API | Image endpoint | Model results | Image counts as 3 units |

## Supervisor

**Best for:** communities and platforms that moderate text, images and video together and want one set of labels and one bill.

Send a base64 image to the same endpoint you use for text. Images are billed at 1 credit per byte, the Observer rate, whichever model you pick; if the image contains readable text, that text is billed at your model's normal rate. Within Premium (£13.99 a month, 90,000,000 credits) a 200 KB image is roughly 200,000 credits by that arithmetic, so image-heavy traffic uses the allowance much faster than text does. That is derived from the per-byte rate, not a published quote. The same API takes [video](/blog/video-moderation) too. Context handling and the 16 labels are described in our [roundup](/blog/best-content-moderation-apis-2026).

We have not verified which of the 16 labels are produced from image content versus text read from the image, so test your own image set in the [live demo](https://supervisor.gg/demo) before assuming coverage.

## OpenAI

**Best for:** free image screening alongside text.

`omni-moderation-latest` accepts text and images and "doesn't classify audio". Images can be up to 20 MB. The guide's example flags violence in an image with a score above 0.8. One secondhand point we could not verify directly from the guide text: which categories accept images and which are text-only. Check the category table before you rely on a given category for images. The guide also says not to send known or suspected CSAM to the endpoint.

## Azure AI Content Safety

**Best for:** Azure teams that want severity-graded image results.

The image API covers the same four categories as text (hate, sexual, violence, self-harm). The image model "only returns severities 0, 2, 4, and 6". Limits: 4 MB maximum file size, dimensions between 50 x 50 and 7,200 x 7,200 pixels, formats JPEG, PNG, GIF, BMP, TIFF or WEBP. List price in the Azure Retail Prices API is $0.75 per 1,000 images (USD, East US), and the F0 free tier allows 5,000 images a month at 5 requests per second. A multimodal image-plus-text API exists in preview.

## AWS: Amazon Rekognition

**Best for:** AWS users who want a detailed label hierarchy and custom adapters.

Rekognition uses a three-level taxonomy; AWS recommends using levels 1 and 2 for moderation. Top-level groups include explicit content, non-explicit nudity, swimwear or underwear, violence, visually disturbing content, drugs and tobacco, alcohol, rude gestures, gambling and hate symbols. It can also flag animated or illustrated content. Input is PNG or JPEG, as base64 bytes (5 MB) or an S3 object (15 MB). `MinConfidence` defaults to 50 percent. Custom Moderation lets you train an adapter on your own annotated images. The list price for the first million images a month is $0.001 per image (USD, US East), with cheaper tiers at volume; for higher tiers AWS's data placed `DetectModerationLabels` in two different price groups, so check the pricing page. AWS notes its moderation APIs don't detect whether an image includes illegal content such as CSAM.

## Hive

**Best for:** organisations that want a large visual taxonomy and are happy to deal with sales.

Hive's visual moderation covers five groups: sexual content, violent imagery, drugs, hate imagery and image attributes, with a brand-safety section in addition. Formats: gif, jpg, png, webp. Its pricing page and its docs disagree on whether visual moderation is self-serve or needs an annual contract, so confirm pricing directly with Hive.

## Sightengine

**Best for:** image-first products that want a wide class list and public self-serve plans.

The docs list 136 classes across 26 models (the pricing page says 150+). Standard models include nudity and adult content (31 classes), violence, weapons, gore, hate and offensive, and self-harm, with restricted topics such as drugs, alcohol, tobacco, gambling and money, plus text-in-image moderation. Plans: free (2,000 operations a month, 500 a day), Starter at $29 and Pro at $99 a month, one operation for running nudity detection on an image. Image size is 12 MB on the plans shown.

## Moderation API

**Best for:** teams that want image moderation plus a review queue.

Has a dedicated `/moderate/image` endpoint, and images count as 3 units against your quota (text counts 1). Basic is $79 a month for 10,000 units. The homepage list of models includes NSFW, self-harm and sensitive topics.

## Honest notes on choosing

- **Size and format limits matter more than they look.** A 4 MB cap (Azure) or 5 MB bytes cap (Rekognition) forces resizing; the Supervisor Discord bot downsizes images before sending them.
- **Output style differs.** Some return a score per class, Azure returns severities, Supervisor returns labels and a flag.
- **Check what the free tier is for.** Several free tiers are for testing, not production.
- **Test on your own images**, especially the borderline ones.

## Sources

[OpenAI](https://developers.openai.com/api/docs/guides/moderation), [Azure region availability and limits](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/region-availability), [Azure harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories), [Rekognition moderation](https://docs.aws.amazon.com/rekognition/latest/dg/moderation-api.html), [Rekognition limits](https://docs.aws.amazon.com/rekognition/latest/dg/limits.html), [Hive visual moderation](https://docs.thehive.ai/docs/visual-content-moderation), [Hive pricing](https://thehive.ai/pricing), [Sightengine classes](https://sightengine.com/docs/image-video-moderation-classes-and-concepts), [Sightengine pricing](https://sightengine.com/pricing), [Moderation API](https://moderationapi.com/).

Send a few of your own borderline images to the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
