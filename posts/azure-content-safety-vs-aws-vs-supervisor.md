---
title: "Azure Content Safety vs AWS moderation vs Supervisor"
date: 2026-10-26
description: "Azure AI Content Safety, AWS (Rekognition and Comprehend) and Supervisor compared from official docs and pricing data: categories, media, limits and what each costs."
---

# Azure Content Safety vs AWS moderation vs Supervisor

**Bottom line:** Azure and AWS are cloud building blocks, so the usual advice holds: use the one on your cloud. Azure gives you one service for text and images with severity levels. AWS splits the job: Rekognition for images and stored video, Comprehend for text toxicity. **Supervisor** is one API across text, images and video with community-oriented labels and a Discord bot, but it is a paid third-party service with no cloud-native identity integration. Pick by where you already run and what content you moderate.

Read from vendor docs and pricing data on 26 October 2026. We have not benchmarked any of them.

## The short answer

- **Azure** if you are on Azure and want graded severity, blocklists and one text-and-image service.
- **AWS** if you are on AWS and need image and stored-video moderation, custom adapters, or text toxicity scores.
- **Supervisor** if you want one provider-neutral API with scams, spam and context, and do not need cloud-native integration.

## At a glance

| | Azure AI Content Safety | AWS (Rekognition and Comprehend) | Supervisor |
| --- | --- | --- | --- |
| Text | Yes, 10K characters per call | Comprehend: up to 10 strings of 1 KB | Yes |
| Images | Yes, 4 MB | Rekognition, PNG or JPEG, 5 MB bytes or 15 MB in S3 | Yes |
| Video | Not in the pages we read | Stored video, async, up to 10 GB and 6 hours | Up to 60 seconds, 10 MB |
| Labels | Hate, sexual, violence, self-harm | Text: 7 toxicity labels. Images: 3-level taxonomy | 16 labels |
| Output | Severity 0 to 7 (image 0, 2, 4, 6) | 0 to 1 scores (text), confidence (images) | Flag and labels |
| Customisation | Blocklists | Rekognition custom moderation adapters | `enabled_labels` |
| Throughput | F0 5 RPS; S0 1,000 requests per 10 seconds | Comprehend 25 TPS (adjustable); Rekognition image 50 TPS in three regions | Not published here |
| Price (USD) | $0.375 per 1,000 text records, $0.75 per 1,000 images | $0.0001 per 100-char unit (text); $0.001 per image; $0.10 per video minute | £13.99 a month (GBP) |
| SDKs | Python, .NET, Java, JavaScript | 10 SDKs listed (incl. Python, Java, Go, JS, .NET) | Python, JavaScript, Go, Rust, Java |

## Azure AI Content Safety

Text and image APIs, four categories, severity-graded. It adds Prompt Shields, groundedness and protected-material detection for LLM apps. Authentication supports keys or Microsoft Entra ID. Trained and tested languages: Chinese, English, French, German, Italian, Japanese, Portuguese and Spanish. The free F0 tier allows 5,000 text records and 5,000 images a month. Prices above come from the Azure Retail Prices API (USD, East US), because the public pricing page rendered placeholders when fetched. One caution: Custom categories (standard) is documented as retiring on 1 September 2026; the page still says preview, so check its status before depending on it.

## AWS

**Comprehend** `DetectToxicContent` scores seven labels (graphic, harassment or abuse, hate speech, insult, profanity, sexual, violence or threat) from 0 to 1 plus an overall score. Its language documentation contradicts itself (twelve codes listed, but "English is the only supported language"). Pricing is per 100-character unit with a 3-unit minimum per request.

**Rekognition** moderates images with a three-level taxonomy and confidence per label (default minimum 50 percent) and offers custom moderation adapters. Stored video is analysed asynchronously. The free tier mentions 1,000 images a month. AWS states its moderation APIs don't detect illegal content such as CSAM. The offer data places image moderation in two price groups with matching first tiers, so we quote only $0.001 for the first million.

## Supervisor

One endpoint family for text, images and video; 16 labels including spam, promotional, scam and illegal; `include_context`; `implicit_labels`; three model tiers; half-price batches; a username endpoint; a Discord bot. Premium costs £13.99 a month for £120 of credits. You give up cloud-native billing and IAM, and you get a provider-neutral API with a flat monthly fee. No audio, no stored-video scale (60 seconds, 10 MB).

## Which to choose

| Your situation | Choose |
| --- | --- |
| Azure shop, text and images | Azure |
| AWS shop, long stored videos | AWS Rekognition |
| AWS shop, need text toxicity scores | Comprehend |
| Cloud-neutral, community moderation | Supervisor |
| Custom visual categories you can train | AWS Rekognition adapters |

Sources: [Azure overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview), [Azure harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories), [Azure limits](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/region-availability), [Comprehend DetectToxicContent](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html), [Comprehend pricing](https://aws.amazon.com/comprehend/pricing/), [Rekognition moderation](https://docs.aws.amazon.com/rekognition/latest/dg/moderation-api.html), [Rekognition limits](https://docs.aws.amazon.com/rekognition/latest/dg/limits.html), [Rekognition pricing](https://aws.amazon.com/rekognition/pricing/).

Try the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
