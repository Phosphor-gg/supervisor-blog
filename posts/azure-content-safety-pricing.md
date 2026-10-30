---
title: "Azure AI Content Safety pricing: what it costs and how Supervisor compares"
date: 2026-10-26
description: "Azure AI Content Safety has a free tier and USD list prices per 1,000 records. Here is what the Azure Retail Prices API shows, how Supervisor's per-byte pricing compares, and where each is cheaper."
---

# Azure AI Content Safety pricing: what it costs and how Supervisor compares

**Bottom line:** Azure AI Content Safety has a free tier of 5,000 text records and 5,000 images a month, then a list price of $0.375 per 1,000 text records and $0.75 per 1,000 images (USD, East US). Supervisor is billed per byte, so it can be cheaper for very short messages and is much more expensive for longer text and for images. Run your own numbers, because message length decides it.

## Where these Azure prices come from

Microsoft's [pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/) did not show dollar amounts when we read it. It rendered placeholders such as "$- per 1,000 text records". So every Azure price here comes from the [Azure Retail Prices API](https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices), in **USD, for the `eastus` region**, as read on 26 October 2026. Other regions carry different figures for some meters, and your bill may differ with currency, agreement or region. Check your own region before budgeting.

In that API the product is listed under the service name "Foundry Tools" and product name "Content Safety".

## What Azure charges

| Meter | List price (USD, eastus) |
|---|---|
| Free tier, text | 5,000 text records a month |
| Free tier, images | 5,000 images a month |
| Standard text | $0.375 per 1,000 text records |
| Standard images | $0.75 per 1,000 images |
| Commitment tier, text, 1M records | $338 per month |
| Commitment tier, text, overage | $0.338 per 1,000 records |
| Commitment tier, images, 250K | $169 per month |
| Commitment tier, images, overage | $0.675 per 1,000 images |

Notes from Microsoft's own pages:

- **What a record is:** "A text record in the S tier contains up to 1,000 characters as measured by Unicode code points." Longer inputs count one record per 1,000 characters, so a 7,500 character input is 8 records. A 100 character message is one record.
- **Free tier limit:** usage stops when you reach it on the free tier.
- **Bundled features:** the pricing page lists text moderation, Prompt Shields, protected material detection and groundedness detection together under text, with no separate price shown.
- **Not priced here:** we found no meter for custom categories and are not quoting a price. Container commitment meters also exist and we did not extract their prices.
- **Rate limits:** the free tier is 5 requests per second; the standard tier is 1,000 requests per 10 seconds for the moderation APIs, with higher rates available on request.

## What Supervisor charges

Premium is £13.99 a month (£83.85 a year, £179.65 for three years) with £120 of credits. Text costs about £0.0014, £0.0027 or £0.0055 per KB on Observer, Sentinel (default) or Arbiter. Images cost about £0.0014 per KB on any model. Batches of two or more are half price. New accounts get £0.10 of free credits, usable for 7 days from the first moderated message. Free credits work on the Observer model for text only; context, images, video and the larger models need Premium or the trial.

## The comparison, honestly

The two currencies differ, so the figures below are nominal and not converted. Convert at today's rate before concluding anything.

| One check | Azure standard | Supervisor Observer | Supervisor Sentinel | Supervisor Arbiter |
|---|---|---|---|---|
| 100 character text | $0.000375 | about £0.00013 | about £0.00027 | about £0.00053 |
| About 1,000 character text | $0.000375 | about £0.0014 | about £0.0027 | about £0.0055 |
| 100 KB image | $0.00075 | about £0.14 | about £0.14 | about £0.14 |

(Supervisor figures are our arithmetic from the per-KB rates. Azure figures are the list price divided by 1,000.)

What that means:

- **Short chat messages:** Azure rounds every message up to a whole 1,000 character record, and Supervisor bills the actual bytes. For messages around 100 characters, Supervisor's default model is nominally cheaper per message, and Premium's allowance covers about 450,000 of them a month. The same volume on Azure standard is 450,000 records, $168.75 at list price.
- **Longer text:** the gap reverses. At about 1,000 characters Supervisor Sentinel is roughly seven times Azure's nominal price. The Premium allowance covers about 45,000 such messages on Sentinel.
- **Images:** this is where we are most expensive. Azure prices per image. Supervisor prices per byte, so a 100 KB image is about 180 times Azure's nominal price, before currency conversion. The Premium allowance covers a little under 900 images of that size.
- **Free tier:** Azure gives you 5,000 text records and 5,000 images a month free. Supervisor does not have a standing free tier for new accounts, only the signup credits and a trial.
- **Batch:** Supervisor halves the price for batches of two or more. We did not find a batch discount in what we read for Azure.

## What the price difference buys

Azure classifies four categories (hate, sexual, violence, self-harm) with severity levels. Supervisor has 16 labels including spam, promotional, scam and illegal, `include_context` for messages that need conversation history, `implicit_labels`, video, translation of non-English messages before classification, three model tiers, a username endpoint, five SDKs and a Discord bot. If you need none of that, Azure's pricing is hard to argue with. See [Supervisor vs Azure AI Content Safety](/blog/supervisor-vs-azure-content-safety) for the full comparison.

Estimate your own cost with the [live demo](https://supervisor.gg/demo) and the [API docs](/docs/integrations/api), or [create a free account](https://supervisor.gg).

## Sources

- Microsoft, [Azure AI Content Safety pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/)
- Microsoft, [Azure Retail Prices API](https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices) (USD, eastus, read 26 October 2026)
- Microsoft, [Content Safety overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview) (rate limits, pricing tiers)
- Supervisor, [API reference: credits and billing](/docs/integrations/api)
