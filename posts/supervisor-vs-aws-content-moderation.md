---
title: "Supervisor vs AWS content moderation: Comprehend and Rekognition compared"
date: 2026-10-26
description: "Amazon Comprehend and Rekognition are pay-per-use building blocks for AWS teams. Supervisor is one moderation API with 16 labels, context flagging, and text, image and video together. An honest comparison."
---

# Supervisor vs AWS content moderation: Comprehend and Rekognition compared

**Bottom line:** if you are already on AWS and only need toxic-text scores or visual categories, use Comprehend and Rekognition. If you need scams, spam, self-harm and illegal content flagged, want to know when a message needs conversation context, or want text, images and video behind one API, **Supervisor** covers that. Supervisor is a paid subscription and can cost more than pay-per-use AWS in some cases, particularly for images.

AWS has no single moderation product. Text goes to Amazon Comprehend toxicity detection and images and video go to Amazon Rekognition content moderation. This post compares that pair with Supervisor.

## What AWS gives you

**Comprehend toxicity detection** takes up to 10 text strings of up to 1 KB each per request and returns an overall toxicity score and scores for seven labels: graphic, harassment or abuse, hate speech, insult, profanity, sexual, and violence or threat ([API reference](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_ToxicContent.html)).

**Rekognition content moderation** returns labels from a three-level taxonomy with confidence scores for images and stored video ([guide](https://docs.aws.amazon.com/rekognition/latest/dg/moderation-api.html)). It supports custom moderation adapters and human review through Amazon Augmented AI, and stored videos up to 10 GB and 6 hours.

Both are billed per use. Both return scores, and you choose the thresholds.

## What Supervisor gives you

Supervisor is a moderation API built for communities, games and platforms. One endpoint takes text or an image, and a video endpoint takes short clips.

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "stop it",
    "model": "sentinel",
    "include_context": true
  }'
```

```json
{
    "flagged": false,
    "labels": [],
    "needs_context": true,
    "context_labels": ["harassment"]
}
```

That response is the point: the message is not flagged on its own, but Supervisor tells you it needs the surrounding conversation and which label it might fall under.

## Side by side

| | AWS (Comprehend + Rekognition) | Supervisor |
| --- | --- | --- |
| Text labels | 7 toxicity labels | 16 labels |
| Scam, spam, promotional, self-harm, illegal | Not in Comprehend's label list | Included |
| Context flagging | Not found in the API reference | `include_context`: `needs_context`, `context_labels` |
| Implicit harm | Not found in the API reference | `implicit_labels` |
| Output | Scores per label | `flagged` plus the labels that triggered it |
| Images | Rekognition, PNG and JPEG | Base64 image in the same endpoint |
| Video | Stored video up to 10 GB and 6 hours, asynchronous | Up to 60 s and 10 MB, up to 20 frames analysed |
| Non-English text | Check AWS's language documentation | Translated before classification, including slang and mixed-language |
| Model choice | No tier selection found in the API references | Three tiers: Observer, Sentinel, Arbiter |
| Batch | Up to 10 strings per Comprehend request | Batch endpoint, half price for batches of two or more |
| Username checks | Not found in the API references | Dedicated `/username` endpoint |
| SDKs | Many languages | Python, JavaScript, Go, Rust, Java |
| Discord bot | Not part of these APIs | Yes, ready-made |
| Custom-trained adapters | Rekognition | Not covered here |
| Human review | Amazon Augmented AI | Not covered here |
| Pricing | Pay per use | One plan, £13.99 a month |

## The differences that matter

### Labels

Comprehend's seven labels are all toxicity-shaped. Communities usually have a different problem: scams, spam, self-promotion and self-harm are often bigger than insults. Supervisor returns 16 labels in one call: profanity, toxicity, harassment, hate, insult, sexual, sexual (unlawful), sexual (explicit), sensitive, violence, self-harm, medical, spam, promotional, scam and illegal. You can restrict a request to the ones you care about with `enabled_labels`.

AWS is upfront about one boundary: Rekognition's image and video moderation APIs do not detect whether an image includes illegal content such as CSAM ([AWS documentation](https://docs.aws.amazon.com/rekognition/latest/dg/moderation-api.html)).

### Context

A lot of harassment is a short message that only makes sense in a thread. Supervisor's `include_context` option tells you when to look at history instead of guessing. We did not find an equivalent in the Comprehend API reference, so with AWS you would build that logic yourself.

### Implicit harm

`implicit_labels` covers content that is harmful without saying so outright. We did not find an equivalent in the AWS API references.

### Text, image and video together

With AWS you integrate two services with different limits and billing units. Supervisor handles text and images on one endpoint and video on another, under one key and one plan. Rekognition wins on scale of stored media: ten gigabyte, six hour files are outside what Supervisor accepts.

### Languages

Supervisor translates non-English messages before classifying them, including slang and mixed-language messages. AWS's Comprehend API reference lists twelve language codes and, on the same page, says English is the only supported language, so check which applies to you before relying on it.

### Where Supervisor is weaker

- **Stored media at scale.** Rekognition handles files Supervisor will not.
- **Customisation.** Rekognition lets you train custom adapters and plug in human review. We have not covered equivalents here.
- **Visual taxonomy depth.** Rekognition's three-level hierarchy is detailed, and you pick the level.
- **Price on images.** Supervisor bills images by file size. A 100 KB image costs about £0.14 according to our docs. AWS bills per image.
- **Low volume.** A subscription is a poor deal for a small side project; pay per use is cheaper there.
- **Not in AWS.** If your access control and billing must stay inside AWS, a separate vendor adds work.

## Price

AWS has no minimum. Comprehend charges $0.0001 per 100 characters in its first tier, with a 300 character minimum per request. Supervisor is £13.99 a month for 90 million credits, which covers roughly 450,000 messages of 100 bytes on Sentinel. We worked through the numbers in the [pricing post](/blog/aws-content-moderation-pricing), including where AWS is cheaper.

## So which should you use?

- **Use AWS** if you are already on AWS, your policy is toxicity plus visual categories, and you want custom adapters or long stored video.
- **Use Supervisor** if you need broad labels, context flagging, implicit harm, translated multilingual handling or one integration, and a flat monthly plan suits you.
- **Use both** if Rekognition handles your archives and Supervisor handles live community text.

Test with your own content: paste a message AWS misses into the [live demo](https://supervisor.gg/demo), read the [API reference](https://supervisor.gg/docs/integrations/api), or [create a free account](https://supervisor.gg) and get an API key. See also the [AWS alternatives roundup](/blog/aws-content-moderation-alternatives) and the [review](/blog/aws-content-moderation-review).

## Sources

- [Comprehend toxic content labels](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_ToxicContent.html) and [DetectToxicContent](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html)
- [Rekognition moderation API](https://docs.aws.amazon.com/rekognition/latest/dg/moderation-api.html) and [limits](https://docs.aws.amazon.com/rekognition/latest/dg/limits.html)
- [Comprehend pricing](https://aws.amazon.com/comprehend/pricing/)
