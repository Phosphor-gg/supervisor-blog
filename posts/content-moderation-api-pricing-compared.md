---
title: "Content moderation API pricing compared in 2026"
date: 2026-10-26
description: "What OpenAI, Azure, AWS, Hive, Sightengine, Moderation API, Llama Guard and Supervisor actually charge, read from vendor pages, with each price's source and currency and the arithmetic shown."
---

# Content moderation API pricing compared in 2026

**Bottom line:** OpenAI's moderation endpoint is free, and nothing here beats free. Past that, the billing unit decides your bill: per 1,000 records, per 100 characters, per image, per operation, per message or per byte. **Supervisor** is the odd one out, a flat £13.99 a month for a credit allowance that you spend by the byte. That makes it more expensive than pay-per-use APIs at low volume and potentially cheaper at high volume with short messages, but it is not cheaper than free, and longer messages use the allowance faster. Work it out with your own message size.

Every figure was read from the vendor's own page on 26 October 2026. We do not convert currencies, because a comparison that quietly converts is one you cannot check. Prices change, so check before you buy.

## The table

| Vendor | Price | Unit | Currency | Source |
| --- | --- | --- | --- | --- |
| OpenAI | Free | The moderation endpoint | n/a | [Moderation guide](https://developers.openai.com/api/docs/guides/moderation) |
| Azure AI Content Safety | $0.375 text, $0.75 images | Per 1,000 (text record = 1,000 characters) | USD, East US list price | Azure Retail Prices API |
| Azure commitment tier | $338 a month text, $169 a month images | Named 1M text and 250K image units | USD, East US | Azure Retail Prices API |
| AWS Comprehend toxicity | $0.0001 | Per 100-character unit, first 10M units a month, 3-unit minimum per request | USD, US East | AWS Price List offer file and [pricing page](https://aws.amazon.com/comprehend/pricing/) |
| AWS Rekognition images | $0.001 | Per image, first million a month | USD, US East | AWS Price List offer file |
| AWS Rekognition stored video | $0.10 | Per minute | USD, US East | AWS Price List offer file |
| Sightengine Starter | $29 a month | 10,000 operations, then $0.002 each | "$" (currency not stated) | [Sightengine pricing](https://sightengine.com/pricing) |
| Sightengine Pro | $99 a month | 40,000 operations, then $0.002 each | "$" (currency not stated) | [Sightengine pricing](https://sightengine.com/pricing) |
| Moderation API Basic | $79 a month | 10,000 messages, then $2.50 per 1,000 | USD | [Moderation API pricing](https://moderationapi.com/pricing) |
| Moderation API Growth | Price not verified | 100,000 messages, then $1.00 per 1,000 | USD | [Moderation API pricing](https://moderationapi.com/pricing) |
| Llama Guard | No API price | Your own hardware | n/a | [Model card](https://huggingface.co/meta-llama/Llama-Guard-4-12B) |
| Supervisor Premium | £13.99 a month, £83.85 a year | 90,000,000 credits; text costs 1, 2 or 4 credits per byte by model | GBP | Supervisor billing system |

### Notes on each row

- **Azure.** The public pricing page shows placeholders instead of amounts when fetched, so these figures come from Microsoft's Retail Prices API, which lists the product under "Foundry Tools". Other regions differ in places. The F0 free tier allows 5,000 text records and 5,000 images a month.
- **AWS.** Comprehend's offer data also lists lower per-unit rates at higher volumes. Its pricing page and offer file disagree about whether the tier above 100 million units is published, so we left that tier out. For Rekognition, the offer data lists `DetectModerationLabels` under two price groups; both charge $0.001 for the first million images, and they diverge at volume, so we only quote the first tier. We did not verify AWS's free-tier duration. AWS bills in many other regions at different rates.
- **Hive.** Hive's pricing page lists self-serve rates (after a 100 requests a day limit) and shows "Contact Sales" for higher limits, CSAM detection and more. Its docs, meanwhile, say text and visual moderation require an annual contract. Because the two disagree, we have left Hive's prices out of the table: ask Hive for a quote. Hive also lists "$50+ in Free Credits after adding a payment method".
- **Sightengine.** One operation is, for example, running nudity detection on an image. How many operations a text request uses depends on how many models you enable (an example response with two text models shows 2 operations), and the FAQ answer on text pricing was not readable in the page we fetched. We do not give a per-message text price for that reason. A free tier of 2,000 operations a month exists.
- **Moderation API.** Quota units: text 1, audio 2, images 3, and video from 3 upward depending on length and models. We could not verify the Growth plan's monthly price from the live page, so we omit it. Free Hobby plan: 100 messages a month.
- **Llama Guard.** The model is free to download behind a licence gate. Hosting cost is yours, and we found no official figure.
- **Supervisor.** Credits are 1, 2 and 4 per byte of text for Observer, Sentinel and Arbiter. Images bill at 1 credit per byte whatever the model, and video frames at 25 percent of that. Batches of two or more cost half. New accounts get 187,500 free credits for 7 days from the first moderated message. Free credits work on the Observer model for text only; context, images, video and the larger models need Premium or the trial.

## Worked example: short messages

Take a stream of short text messages of about 100 bytes each, on Supervisor's default Sentinel model (2 credits per byte, so 200 credits a message). This is derived arithmetic, not a vendor quote. Each message is under 1,000 characters, so it is one record on Azure.

| Monthly messages | OpenAI | Azure | --- | --- | --- | --- | --- | --- |
| 10,000 | Free | $3.75 | $5.00 | $79 | £13.99 flat (uses 2,000,000 of 90,000,000 credits) |
| 450,000 | Free | $168.75 | $225.00 | $1,179 ($79 plus 440,000 over at $2.50 per 1,000) | £13.99 flat (uses the whole allowance) |

What the example shows:

- At 10,000 short messages, the pay-per-use APIs cost less than Supervisor's flat fee. Supervisor costs more per message at this volume, and OpenAI costs nothing.
- At 450,000 short messages, 450,000 messages is exactly what the Premium allowance covers on Sentinel, so the flat fee works out at about £0.031 per 1,000 messages. That is the best case and it assumes you use all of it.
- We left out AWS and Sightengine because their text billing rules were ambiguous or unreadable in the pages we fetched.
- Currencies differ (USD or "$" against GBP), so we do not total them.

## The same example with longer messages

Supervisor bills by byte, so size matters more than it does on a per-record API. A 1,000 byte message on Sentinel is 2,000 credits, so the 90,000,000 credit allowance covers 45,000 of them, a tenth of the 450,000 short-message figure. On Azure, a 1,000 character text is still one record. Long messages are where per-byte billing is least favourable, and Observer (1 credit per byte) doubles the count. Batching halves the cost again. If most of your content is long, price it before you commit.

## Which pricing model suits you

- **Low or spiky volume:** pay-per-use or free tiers (OpenAI, Azure, Moderation API's free plan).
- **Steady volume of short messages:** a flat allowance like Supervisor's can win, because the fee does not grow with each message.
- **Image and video heavy:** compare per image and per minute; AWS publishes both.
- **You have GPUs already:** Llama Guard has no per-call fee.
- **You value what you get for the money:** price is only half the comparison. Supervisor includes 16 labels, context handling, text, image and video, and a Discord bot in the one plan; whether that is worth it depends on whether you need those.

## Sources

[OpenAI](https://developers.openai.com/api/docs/guides/moderation), [Azure pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/) and the Azure Retail Prices API, [AWS Rekognition pricing](https://aws.amazon.com/rekognition/pricing/), [AWS Comprehend pricing](https://aws.amazon.com/comprehend/pricing/), [Hive](https://thehive.ai/pricing), [Sightengine](https://sightengine.com/pricing), [Moderation API](https://moderationapi.com/pricing), [Llama Guard 4](https://huggingface.co/meta-llama/Llama-Guard-4-12B).

Try Supervisor in the [live demo](https://supervisor.gg/demo), check the rates in the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
