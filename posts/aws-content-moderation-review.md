---
title: "AWS content moderation review: Comprehend and Rekognition, what they do well and where they run out"
date: 2026-10-26
description: "An honest review of Amazon Comprehend toxicity detection and Amazon Rekognition content moderation: strengths, limits from AWS's own documentation, and who each one suits."
---

# AWS content moderation review: Comprehend and Rekognition, what they do well and where they run out

**Bottom line:** the AWS pair is a solid, pay-per-use choice for teams already on AWS. Rekognition is the more capable half, with a detailed visual taxonomy, custom adapters, human review and long stored-video support. Comprehend toxicity detection is a narrower tool: text only, seven labels, scores rather than decisions. Both leave you to build thresholds, context handling and anything beyond toxicity and visual categories.

This review uses AWS's own documentation. Where its pages disagree, we say so rather than pick a side.

## What it is

AWS moderation is two services you combine:

- **[Amazon Comprehend toxicity detection](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html)** analyses text. You send a list of up to 10 strings, each up to 1 KB, and get back an overall toxicity score plus a score per label.
- **[Amazon Rekognition content moderation](https://docs.aws.amazon.com/rekognition/latest/dg/moderation.html)** analyses images and video for inappropriate, unwanted or offensive content.

## What it does well

**Rekognition's taxonomy is detailed.** It uses a [three-level hierarchy](https://docs.aws.amazon.com/rekognition/latest/dg/moderation-api.html) of categories, and AWS recommends using the first and second levels for moderation and the third only to exclude specific concepts you do not want to moderate. That makes it practical to tune: block explicit nudity but allow swimwear, for instance.

**You control the confidence threshold.** `MinConfidence` runs from 0 to 100 and defaults to 50. AWS warns that going below 50 is likely to return many false positives. A documented trade-off you can set yourself is better than a hidden one.

**Custom moderation and human review exist.** Rekognition lets you train a custom moderation adapter by uploading and annotating your own images, and it integrates with Amazon Augmented AI for human review workforces.

**It handles large stored media.** Rekognition Video analyses stored videos up to 10 GB and 6 hours long, and bulk image analysis handles batches of up to 10,000 images, per AWS's [limits page](https://docs.aws.amazon.com/rekognition/latest/dg/limits.html). If you moderate archives or long recordings, that is a real advantage.

**It recognises animated and illustrated content.** The API can identify when content is animated (video game, animation) or illustrated (drawing, painting, sketches), which helps you treat fiction differently from photographs.

**Many SDKs and a familiar platform.** Both APIs list SDKs for the AWS CLI, .NET, C++, Go, Java, JavaScript, Kotlin, PHP, Python and Ruby. If your infrastructure, billing and access control already live in AWS, adding these is a small step.

**Pay per use.** There is no subscription. See the [pricing breakdown](/blog/aws-content-moderation-pricing) for how each service is billed.

## Where it runs out

**Comprehend's labels are toxicity labels.** The seven names are graphic, harassment or abuse, hate speech, insult, profanity, sexual, and violence or threat. There is no scam, spam, promotional, self-harm or medical label. If those matter to your community, you need something else.

**Scores, not severity bands or decisions.** Both services return numeric scores or confidences. That is flexible, but you own the threshold, the escalation logic and the retuning when content changes.

**Text and media are separate integrations.** Comprehend handles text and Rekognition handles images and stored video. They have different request shapes, limits and billing units. The Rekognition API accepts PNG and JPEG images, and moderation for video is an asynchronous job on stored files. We found no live-stream moderation among Rekognition's streaming video features on [its endpoints page](https://docs.aws.amazon.com/general/latest/gr/rekognition.html).

**Per-request text limits.** Comprehend's limit is 1 KB per string and 10 strings per request. Longer content has to be split by you.

**Rekognition is explicit about its scope.** AWS says it does not claim to be an exhaustive filter, and that its image and video moderation APIs do not detect whether an image includes illegal content such as CSAM. That is honest, and it means you need another control for that category.

**No conversation-context mechanism that we could find.** The Comprehend API takes independent text segments. We did not find a parameter for conversation history or for signalling that a message needs context.

**Language support is unclear.** The Comprehend API reference lists twelve language codes for `LanguageCode` and, in the same page, says English is currently the only supported language. We cannot tell you which is right. Check with AWS for the languages you need before building on it.

**Throughput has defaults to plan around.** The default Comprehend toxicity quota is 25 requests per second per region, adjustable. Rekognition's default image-moderation quota is 50 transactions per second in US East (N. Virginia), US West (Oregon) and Europe (Ireland), and 5 in many other regions, adjustable through a support case.

## Where Supervisor fills gaps, and where it does not

Supervisor is our product, so read this as a vendor's view.

| Need | AWS | Supervisor |
| --- | --- | --- |
| Scam, spam, promotional, self-harm, illegal labels | Not in Comprehend's label list | Part of 16 labels |
| Flag a message that needs conversation | Not found in the API reference | `include_context` returns `needs_context` and `context_labels` |
| Harm that is implied | Not found in the API reference | `implicit_labels` |
| Text, image and video in one API | Two services | One API |
| Non-English text | Check language support | Translated before classification, including slang and mixed-language |
| Custom-trained adapters | Rekognition | Not covered here |
| Long stored video (up to 10 GB, 6 hours) | Rekognition | Video up to 60 s and 10 MB |
| Human review workflow | Amazon Augmented AI | Not covered here |
| Pricing | Pay per use | One plan, £13.99 a month |

Supervisor is the better fit when you want broad labels, context and one integration. AWS is the better fit for large stored media, custom adapters and teams that want to stay inside AWS.

## Who AWS moderation is right for

- Teams already running on AWS who want to add moderation without a new vendor.
- Products with a clear visual policy, where Rekognition's taxonomy and custom adapters fit.
- Teams with large video or image archives to process asynchronously.

It is a weaker fit if you moderate community chat and need scams, spam and self-harm covered, or if you want a ready-made answer rather than scores to threshold.

## Verdict

Rekognition is a strong, flexible visual moderation service, and Comprehend toxicity detection is a competent text signal with a narrow label set. Run both if you are on AWS and your policy matches them. Add a second layer for what they do not return.

Try your own messages in the [live demo](https://supervisor.gg/demo), read the [API reference](https://supervisor.gg/docs/integrations/api), or [create a free account](https://supervisor.gg).

## Sources

- [Comprehend DetectToxicContent API reference](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html) and [label names](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_ToxicContent.html)
- [Comprehend service quotas](https://docs.aws.amazon.com/general/latest/gr/comprehend.html)
- [Rekognition content moderation guide](https://docs.aws.amazon.com/rekognition/latest/dg/moderation.html) and [moderation API and taxonomy](https://docs.aws.amazon.com/rekognition/latest/dg/moderation-api.html)
- [DetectModerationLabels API reference](https://docs.aws.amazon.com/rekognition/latest/APIReference/API_DetectModerationLabels.html)
- [Rekognition limits](https://docs.aws.amazon.com/rekognition/latest/dg/limits.html) and [endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/rekognition.html)
