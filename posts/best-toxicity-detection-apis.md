---
title: "Best toxicity detection APIs after Perspective"
date: 2026-10-26
description: "Perspective API is shutting down after 2026. Here are the toxicity and abuse detection APIs that are still around, compared from their own docs, with an honest best-for on each."
---

# Best toxicity detection APIs after Perspective

**Bottom line:** if you used Perspective API to score comments for toxicity, you need a replacement before 31 December 2026. Most of the options below score abuse, hate and harassment in text. OpenAI's endpoint is free and a sensible default for LLM apps. Amazon Comprehend has the closest "score per toxicity label" shape. Sightengine and Moderation API have explicit toxic or toxicity classes. **Supervisor**, our own product, is best if toxicity is only part of the problem and you also need scams, spam and messages that cannot be judged without context.

This list was written on 26 October 2026 from each vendor's own documentation. We have not benchmarked these tools against each other, so there is no accuracy ranking here. Perspective's own model card says it "is not intended to be used for fully automated moderation", and the same caution applies to every tool below: treat scores and flags as input to your policy.

Perspective's status, from [perspectiveapi.com](https://www.perspectiveapi.com/): service ends after 2026, it remains active until 31 December 2026, and Jigsaw is not offering migration support. Our [migration guide](/blog/perspective-api-migration-guide) covers the move step by step.

## What toxicity detection tools differ on

- **Label set.** Some give one toxicity score; others split into insult, hate, harassment and profanity.
- **Score or decision.** Perspective returned a score. Some replacements return scores, some return severity bands, some return a flag.
- **Context.** Perspective's model card says its toxicity model "only helps detect toxicity in an individual statement". Check whether a replacement can tell you when a message needs surrounding conversation.
- **Languages.** Read the vendor's list, not the headline. See [our multilingual comparison](/blog/best-multilingual-moderation-apis).
- **Limits.** Text length caps vary from 1,000 characters to 10,000.

## Supervisor

**Best for:** communities and platforms where rudeness is one problem among several.

Supervisor's 16 labels include the toxicity family (toxicity, insult, harassment, hate, profanity) and, beyond it, sexual, sensitive, violence, self-harm, medical, spam, promotional, scam and illegal. You choose which count with `enabled_labels`, so a Perspective migration can start with just the toxicity labels. Set `include_context` and the response includes `needs_context` when a message cannot be judged alone, and `implicit_labels` covers content that is harmful without saying so outright. Non-English text is translated to English before classification, including slang and mixed-language messages.

The response is a decision (`flagged` plus the labels), not a score to threshold, which changes how migration code looks. Three model tiers (Observer, Sentinel, Arbiter) let you trade cost against depth, and batches of two or more cost half as much.

Trade-offs: it is paid (Premium is £13.99 a month with £120 of credits, plus £0.25 of free signup credits usable for 7 days), and it returns labels rather than a 0 to 1 score per attribute. We do not publish accuracy numbers in this post.

## OpenAI moderation endpoint

**Best for:** free screening of text and images in an LLM application.

The categories in OpenAI's guide are harassment (with a threatening subcategory), hate (with threatening), violence, sexual, self-harm and illicit. There is no separate insult or profanity label. It is free, accepts text and images, and returns `flagged`, `categories` and `category_scores`. The guide does not list supported languages. Its own advice: "Treat moderation scores as signals for your application's policy, not as an automatic blocking decision." See our [comparison](/blog/supervisor-vs-openai-moderation).

## Amazon Comprehend toxicity detection

**Best for:** AWS teams that want a per-label score like Perspective's.

`DetectToxicContent` returns a score from 0 to 1 for each of seven labels (graphic, harassment or abuse, hate speech, insult, profanity, sexual, violence or threat) plus an overall toxicity score, with no severity bands. A request takes up to 10 strings of up to 1 KB each. The default throttle is 25 transactions per second per region and is adjustable. Pricing is per 100-character unit, in USD. The API reference lists twelve language codes but also says "English is the only supported language", so confirm the current position with AWS before relying on non-English text.

## Azure AI Content Safety

**Best for:** Azure teams that want severity levels for hate, sexual, violence and self-harm.

Four categories, each with a 0 to 7 severity scale you can trim to four levels, plus blocklists for your own terms. There is no insult, profanity or generic toxicity label, so a Perspective-style "is this rude" check is not what it was designed for. Text up to 10,000 characters per call. The free F0 tier covers 5,000 text records a month.

## Sightengine

**Best for:** products that need text moderation alongside image and video moderation, with public plans.

Machine-learning text classes: sexual, discriminatory, insulting, violent, toxic and self-harm, each scored 0 to 1. Rule-based classes add profanity, personal information, links, spam, extremism, weapons, drugs and custom blacklists. The ML classes support seven languages (English, French, Italian, Portuguese, Spanish, Russian, Turkish); the rule-based side lists eighteen. There is a free tier of 2,000 operations a month, then $29 a month.

## Moderation API

**Best for:** teams that want toxicity models plus a review queue and rules engine.

The homepage lists ready-made models including toxicity, profanity, hate speech, harassment, self-harm, spam, scams and sensitive topics, and claims 120+ languages. Free Hobby plan of 100 messages a month; Basic is $79 a month for 10,000 messages, with overage at $2.50 per 1,000.

## Hive

**Best for:** larger organisations comfortable with a sales-led contract.

Hive's text classes include sexual, hate, violence, bullying, promotions and spam, ordered by severity from 0 (benign) to 3 (most severe), across roughly 30 languages. Text input is capped at 1,024 characters. Its docs say text moderation requires an annual contract and that smaller customers should use its self-serve vision-language model instead.

## Llama Guard

**Best for:** self-hosting a safety classifier next to an LLM.

Llama Guard 4 predicts labels from a 14-category hazard taxonomy (including hate, and suicide and self-harm) rather than a toxicity score, and it is designed for classifying LLM prompts and responses. Weights are free but gated by licence, and you supply the hardware. It is a different tool from Perspective, not a drop-in.

## Which should you choose?

| Your situation | Start with |
| --- | --- |
| LLM app, want free | OpenAI |
| On AWS, want scores per label | Amazon Comprehend |
| On Azure, want severity | Azure AI Content Safety |
| Text plus images and video, public plans | Sightengine |
| Want review queue and rules engine | Moderation API |
| Community or platform with scams, spam and context | Supervisor |
| Must self-host | Llama Guard |

Whichever you pick, run both old and new side by side before the cut-off and read where they disagree.

## Sources

[Perspective](https://www.perspectiveapi.com/), [OpenAI](https://developers.openai.com/api/docs/guides/moderation), [Comprehend](https://docs.aws.amazon.com/comprehend/latest/APIReference/API_DetectToxicContent.html), [Azure harm categories](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories), [Sightengine text moderation](https://sightengine.com/docs/text-moderation-introduction), [Moderation API](https://moderationapi.com/), [Hive text classification](https://docs.thehive.ai/docs/classification-text), [Llama Guard 4](https://huggingface.co/meta-llama/Llama-Guard-4-12B).

Try Supervisor on messages Perspective used to score in the [live demo](https://supervisor.gg/demo), read the [API reference](/docs/integrations/api), or [create a free account](https://supervisor.gg).
