---
title: "Supervisor vs Azure AI Content Safety: which should you use?"
date: 2026-10-26
description: "Azure AI Content Safety offers four categories with severity levels, blocklists and a free tier. Supervisor offers 16 labels, context, video and a Discord bot, at a higher price for longer text and images. An honest comparison."
---

# Supervisor vs Azure AI Content Safety: which should you use?

**Bottom line:** Azure AI Content Safety is cheaper for longer text and for images, has graded severity and a free tier, and fits teams already in Azure. **Supervisor** costs more there, but covers 16 labels including spam, scam and promotional, flags messages that need conversation context, takes video, and comes with a Discord bot. Pick by the job, not the label count.

We make Supervisor. Azure claims here come from Microsoft's documentation (linked below), and Azure prices from the Azure Retail Prices API in USD for East US. We did not test either product's accuracy or speed, so this post makes no claims about them.

## At a glance

| | Azure AI Content Safety | Supervisor |
|---|---|---|
| Built-in categories | 4: hate, sexual, violence, self-harm | 16 labels |
| Output | Severity numbers (text 0 to 7, image 0, 2, 4, 6) | `flagged` plus `labels` |
| Input types | Text, images, multimodal (preview) | Text, images, video |
| Spam, scam, promotional | Not among the four categories | Yes, labels |
| Context | Not documented in what we read | `include_context`: `needs_context` and `context_labels` |
| Implicit harm | Not documented in what we read | `implicit_labels` |
| Languages | 8 trained and tested, others vary | Non-English translated before classification |
| Custom terms | Blocklists | Not documented in the API (Discord bot has link allow and block lists) |
| Free tier | 5,000 text records and 5,000 images a month | Signup credits, 7 day trial |
| Price shape | Per 1,000 records or images | Per byte, 50% off batches |
| Extras | Prompt Shields, groundedness, protected material | Username endpoint, Discord bot |
| SDKs | Python, .NET, Java, JavaScript | Python, JavaScript, Go, Rust, Java |
| Setup | Azure resource, key or Entra ID | API key from the dashboard |

## What Azure does well

- **Severity.** "The current version of the text model supports the full 0-7 severity scale", so you can threshold per category and per surface. Supervisor's documented response does not give a severity number per category.
- **Blocklists.** Your own terms, with `blocklistNames` and `haltOnBlocklistHit` in the text API.
- **LLM safety features.** Prompt Shields scan for user input attacks on a large language model. There are also groundedness and protected material checks. Supervisor has none of these.
- **Free tier and rate limits.** 5,000 records and images free each month, and a documented limit of 1,000 requests per 10 seconds on the standard tier. We have not verified Supervisor's API rate limits, so we will not compare them.
- **Enterprise fit.** Microsoft Entra ID, managed identity, regions.

## Where Azure's built-in set runs out

Microsoft classifies content "into four categories, hate, sexual, violence, and self-harm". If your abuse is scam links, spam or self-promotion, none of the four is built to flag it. You can use blocklists or custom categories, but you maintain them. (Microsoft's page says custom categories (standard) was due to retire on 1 September 2026, and we could not confirm whether it is still available, so check.) Azure's text classifiers are trained and tested on eight languages, and several features are English only.

## What Supervisor does differently

- **16 labels:** profanity, toxicity, harassment, hate, insult, sexual, sexual (unlawful), sexual (explicit), sensitive, violence, self-harm, medical, spam, promotional, scam and illegal.
- **Context:** send `"include_context": true` and a message like "stop it" can come back `needs_context: true` with `context_labels: ["harassment"]`, telling you to resend it with history.
- **Implicit harm** through `implicit_labels`.
- **Video** (up to 60 seconds, 10 MB, 20 frames analysed, per-frame timestamps) through the same API as text and images. We did not find video input on the Azure Content Safety pages we read, so check Microsoft's API reference if you need it.
- **Language handling:** non-English text is translated before classification, including slang and mixed-language messages. We make no claim about how many languages or how accurately.
- **A ready-made Discord bot,** a username check endpoint, three model tiers and a batch discount.

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "stop it",
    "include_context": true
  }'
```

## Price: the honest part

Azure: $0.375 per 1,000 text records and $0.75 per 1,000 images (list, USD, East US), where a record is up to 1,000 characters. Supervisor: £13.99 a month for £120 of credits, with text at about £0.0014, £0.0027 or £0.0055 per KB (Observer, Sentinel, Arbiter) and images at about £0.0014 per KB.

- **Short messages (about 100 characters):** Supervisor's default model costs about £0.00027 per message, against $0.000375 for Azure's one record. Nominally Supervisor is lower here, but the currencies differ, so convert before relying on it.
- **About 1,000 characters:** Supervisor Sentinel is about £0.0027, roughly seven times Azure's nominal price.
- **Images:** a 100 KB image is about £0.14 on Supervisor against $0.00075 on Azure, about 180 times in nominal figures. This is where we are most expensive by far.

The full table and sources are in [Azure AI Content Safety pricing](/blog/azure-content-safety-pricing).

## Which should you use?

**Azure** if you are in Azure, your policy fits the four categories, you want severity numbers or blocklists, you are building an LLM app that needs Prompt Shields, or image volume is high and cost matters.

**Supervisor** if scams, spam and promotion are as big a problem as overt harm, messages depend on conversation context, you need video or Discord moderation, or you want a decision with labels rather than severity numbers and are fine paying more.

**Both** is reasonable: a cheap first pass, then a second layer for what it misses. Run your real messages through each and read the disagreements.

Try messages in the [live demo](https://supervisor.gg/demo), read the [API docs](/docs/integrations/api), or [create a free account](https://supervisor.gg). More: [Azure review](/blog/azure-content-safety-review), [alternatives](/blog/azure-content-safety-alternatives).

## Sources

- Microsoft, [Content Safety overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview), [harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories), [region availability and limits](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/region-availability), [text quickstart](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/quickstart-text), [custom categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/custom-categories)
- Microsoft, [pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/) and [Azure Retail Prices API](https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices)
- Supervisor, [API reference](/docs/integrations/api)
