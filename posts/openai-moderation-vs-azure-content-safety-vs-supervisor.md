---
title: "OpenAI moderation vs Azure Content Safety vs Supervisor"
date: 2026-10-26
description: "A free endpoint, a cloud service with severity levels, and a paid API for communities. OpenAI, Azure AI Content Safety and Supervisor compared from their own docs."
---

# OpenAI moderation vs Azure Content Safety vs Supervisor

**Bottom line:** OpenAI's endpoint is free and a good default for screening an LLM app. Azure AI Content Safety is the better fit when you live on Azure and want severity levels and blocklists. **Supervisor** costs more than both per message at low volume, and is for communities and platforms that need scams, spam and context handled, plus video. Different jobs, so pick by the job.

Read from vendor docs on 26 October 2026. We have not benchmarked accuracy or speed.

## The short answer

- **Pick OpenAI** if you want free text and image screening and your main risk is harmful content in an AI product.
- **Pick Azure** if you are on Azure and want graded severity, blocklists and Microsoft's identity and SDK tooling.
- **Pick Supervisor** if scams, spam, self-promotion and context matter as much as abuse, or if you need video and a Discord bot.

## At a glance

| | OpenAI | Azure AI Content Safety | Supervisor |
| --- | --- | --- | --- |
| Input | Text, images | Text, images (multimodal preview) | Text, images, video |
| Categories | Sexual, harassment, hate, illicit, self-harm, violence, with subcategories (13 keys in the guide) | Hate, sexual, violence, self-harm | 16 labels including spam, promotional, scam, illegal |
| Output | Flag, categories, scores | Severity 0 to 7 (trimmable), image 0, 2, 4, 6 | `flagged` and labels |
| Custom terms | Not documented in the guide | Blocklists | `enabled_labels` to choose labels |
| Context | Not stated in the guide | Not stated in the pages we read | `include_context` returns `needs_context` |
| Languages | No list published | 8 trained and tested | Translated to English first, no count |
| Price | Free | USD per 1,000 records; F0 free tier | £13.99 a month |
| SDKs | JS, Python, Go, Java, C#, Ruby samples | Python, .NET, Java, JavaScript | Python, JavaScript, Go, Rust, Java |

## OpenAI

The guide says `omni-moderation-latest` accepts text and images and "doesn't classify audio", and that "The moderation endpoint is free to use". It can also return moderation scores alongside a generated response. Scores are described as "signals for your application's policy, not as an automatic blocking decision". The guide does not list languages or moderation-specific rate limits.

Where it runs out for community work: the categories shown have no spam, scam or promotional label. Where it shines: price and simplicity.

## Azure AI Content Safety

Four categories (hate, sexual, violence, self-harm) for text and images, with a severity per category. Text supports a 0 to 7 scale; with `outputType` you can ask for four levels. Blocklists let you add your own terms. The text limit is 10,000 characters per call, images 4 MB. Standard pricing in the Azure Retail Prices API is $0.375 per 1,000 text records and $0.75 per 1,000 images (USD, East US), and the F0 tier gives 5,000 of each a month. Rate limits: F0 is 5 requests per second; S0 is 1,000 requests per 10 seconds. Beyond moderation, Azure offers Prompt Shields and groundedness detection for LLM apps.

Where it runs out: the four-category set leaves out spam, scams and profanity as labels. We did not find a video API on the Content Safety pages we read.

## Supervisor

16 labels, three model tiers (Observer, Sentinel, Arbiter), `include_context` for messages that need the conversation, `implicit_labels` for harm that is not stated outright, video with per-frame timestamps (60 seconds, 10 MB), a batch endpoint at half price, a username check endpoint, SDKs for five languages and a Discord bot.

The honest part on price: it is paid, with no permanent free tier. Premium is £13.99 a month for 90,000,000 credits; Sentinel costs 2 credits a byte, so about 450,000 messages of 100 bytes. At low volume that is more than Azure's $0.375 per 1,000 records, and always more than OpenAI's nothing. See [our pricing comparison](/blog/content-moderation-api-pricing-compared).

## Which to choose

| Your situation | Choose |
| --- | --- |
| AI chatbot, free screening, standard harm categories | OpenAI |
| Enterprise on Azure, need severity bands and blocklists | Azure |
| Community or marketplace, scams and spam are a daily problem | Supervisor |
| Video uploads | Supervisor (Azure's docs we read list no video) |
| Tight budget, low volume | OpenAI, then Azure's F0 |

They are not exclusive. A common pattern is a free classifier as a first filter and a specialised one where the harm is subtle. See our [pairwise comparison with OpenAI](/blog/supervisor-vs-openai-moderation).

## Sources

[OpenAI moderation guide](https://developers.openai.com/api/docs/guides/moderation), [Azure overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview), [Azure harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories), [Azure region availability and limits](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/region-availability), [Azure quickstart](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/quickstart-text), [Azure pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/).

Test your own messages in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
