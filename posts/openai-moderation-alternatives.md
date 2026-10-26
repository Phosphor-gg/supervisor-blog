---
title: "OpenAI moderation endpoint alternatives: when free is not enough"
date: 2026-10-26
description: "OpenAI's moderation endpoint is free and a good default. Here is what it covers, where people outgrow it, and the alternatives worth testing: Azure AI Content Safety and Supervisor."
---

# OpenAI moderation endpoint alternatives: when free is not enough

**Bottom line:** if you only need to classify text and images against OpenAI's published harm categories, the moderation endpoint is free and you probably do not need an alternative. People look elsewhere when they need labels it does not list (spam, scams, promotion), a yes or no decision instead of scores, video, or a documented answer on languages. **Azure AI Content Safety** is the other big cloud option. **Supervisor** is the paid one aimed at communities and platforms, and it costs more.

We make Supervisor, so weigh this accordingly. Every claim about OpenAI below comes from [OpenAI's moderation guide](https://developers.openai.com/api/docs/guides/moderation), and where the guide is silent we say so rather than guess.

## What you get with OpenAI's endpoint

- **Price:** "The moderation endpoint is free to use."
- **Model:** `omni-moderation-latest`, which "accepts text and image inputs. It doesn't classify audio."
- **Images:** files "can be up to 20 MB".
- **Output:** a `flagged` field, per-category booleans and `category_scores`.
- **Categories:** the example response lists 13 keys: sexual, sexual/minors, harassment, harassment/threatening, hate, hate/threatening, illicit, illicit/violent, self-harm, self-harm/intent, self-harm/instructions, violence and violence/graphic.
- **Inline option:** you can pass a `moderation` object on a generation request and get scores for the model input and generated output back together.

That is a strong default, and nothing below changes it. For many projects the right move is to use it and stop.

## Why people look for alternatives

**The category list is a safety list.** None of the 13 keys in the guide's example response is spam, scam or promotional content. If your problem is a marketplace full of scam listings or a community full of self-promotion, you will not find a matching category there. (Self-harm and illicit activity are covered, so those are not gaps.)

**You get scores, and the decision is yours.** OpenAI is explicit: "Treat moderation scores as signals for your application's policy, not as an automatic blocking decision." That is a sensible design, but it means you pick and maintain the thresholds.

**Languages are not documented.** The guide has no statement of supported languages. That is not the same as saying it does badly in other languages. It means there is nothing to check your community against, so test it on your own messages.

**Video is not a listed input.** The guide names text and images only.

**Limits you should read before relying on it.** Do not send known or suspected child sexual abuse material to it: "The API is not designed for CSAM detection or handling and is not a substitute for dedicated child-safety safeguards." Also, if you stream a generated response, "moderation scores arrive after the full generated output is available", and "a refusal or other safety-aware response can still trigger a flag if it discusses harmful content."

**Things we could not verify.** The guide does not state rate limits for the moderation endpoint, a latency figure, or whether you can pass conversation history as context. If any of those matter, ask OpenAI or test it.

## The alternatives

### Azure AI Content Safety

Microsoft's service classifies text and images into four categories, hate, sexual, violence and self-harm, with a severity from 0 to 7 for text. It has a free tier of 5,000 text records and 5,000 images a month, then pay as you go. It adds Prompt Shields, protected material detection, blocklists and custom categories features. You create an Azure resource in a supported region, and the SDKs cover Python, .NET, Java and JavaScript.

Compared with OpenAI it is a paid service after the free tier, but it gives you severity levels and blocklists. Like OpenAI, the four built-in categories do not include spam or scams. See our [Azure AI Content Safety review](/blog/azure-content-safety-review) and [pricing breakdown](/blog/azure-content-safety-pricing).

**Best for:** teams already on Azure, or who want severity levels and custom blocklists.

### Supervisor

Supervisor is a paid moderation API and Discord bot. It is more expensive than a free endpoint, and for longer text and images it is more expensive per message than Azure's standard tier too (we break that down in [Supervisor vs Azure AI Content Safety](/blog/supervisor-vs-azure-content-safety)). What you get for the money:

- **16 labels**, including spam, promotional, scam, self-harm and illegal alongside the usual harm categories.
- **A decision, not just scores:** the response has `flagged` and the `labels` that triggered it.
- **Context:** `include_context` returns `needs_context` and `context_labels` when a message cannot be judged alone.
- **Implicit harm:** `implicit_labels` for content that is harmful without saying so outright.
- **Text, images and video** through one API (video up to 60 seconds and 10 MB).
- **Non-English messages** are translated before classification, including slang and mixed-language messages.
- **Three model tiers** (Observer, Sentinel, Arbiter), a **50% discount** on batches of two or more, a **username check** endpoint, **SDKs** for Python, JavaScript, Go, Rust and Java, and a **ready-made Discord bot**.

Premium is £13.99 a month with 90,000,000 credits. Images are the expensive part: a 100 KB image costs about £0.14. See [OpenAI moderation pricing](/blog/openai-moderation-pricing) for the arithmetic.

**Best for:** communities and platforms where scams, spam and context matter more than cost.

## Quick comparison

| | OpenAI moderation | Azure AI Content Safety | Supervisor |
|---|---|---|---|
| Price | Free per the guide | Free tier, then per record (USD list) | Paid, £13.99 a month Premium |
| Input types | Text, images | Text, images | Text, images, video |
| Built-in categories | 13 listed keys | 4 | 16 |
| Spam, scam, promotional labels | Not in the example response | Not among the four | Yes |
| Output | Scores plus flags | Severity numbers | Decision plus labels |
| Context flag | Not documented | Not documented in what we read | `needs_context` |
| Languages | Not documented | 8 trained and tested, others vary | Translated before classification |

## Do you need to leave OpenAI at all?

Often not. A common setup is to keep the free endpoint as a first pass for the safety categories and add something else for what it does not list. Run both on a sample of real messages for a week and look at the disagreements. That tells you more than any table, including this one.

Try messages from your own community in the [live demo](https://supervisor.gg/demo), read the [API docs](/docs/integrations/api), or [create a free account](https://supervisor.gg) to get an API key.

## Sources

- OpenAI, [Moderation guide](https://developers.openai.com/api/docs/guides/moderation)
- Microsoft, [Azure AI Content Safety overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview) and [harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories)
- Supervisor, [API reference](/docs/integrations/api)
