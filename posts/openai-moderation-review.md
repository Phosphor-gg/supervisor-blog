---
title: "OpenAI moderation endpoint review: a free default and where it runs out"
date: 2026-10-26
description: "An honest review of OpenAI's moderation endpoint from a company that sells a competing product. What it does well, what its own guide says about its limits, and what it does not document."
---

# OpenAI moderation endpoint review: a free default and where it runs out

**Bottom line:** OpenAI's moderation endpoint is free, handles text and images, and returns per-category scores across 13 safety categories. That makes it a very good default. It runs out when you need spam, scam or promotional detection, a decision rather than scores, video, or documented language coverage. Add something else for those, and keep it for what it does well.

We make Supervisor, a paid competitor, so treat this as an interested party's view. Everything about OpenAI below comes from [OpenAI's moderation guide](https://developers.openai.com/api/docs/guides/moderation). We did not test the endpoint, so this review makes no claim about accuracy or speed.

## What it is

OpenAI describes it as a way to "detect harmful content in text and images". The model is `omni-moderation-latest`. You can classify standalone inputs with the moderation endpoint, or request moderation scores alongside a generated response.

## What it does well

**It is free.** "The moderation endpoint is free to use." Nothing we offer beats that, and we say so plainly.

**Text and images in one model.** The model "accepts text and image inputs", with images up to 20 MB.

**A thoughtful category set for safety.** The example response lists 13 keys, with subcategories that matter: `sexual/minors`, `harassment/threatening`, `hate/threatening`, `illicit/violent`, `self-harm/intent`, `self-harm/instructions` and `violence/graphic`. Distinguishing intent and instructions from general self-harm content is useful detail.

**Scores, not just a verdict.** You get `flagged`, `categories` and `category_scores`, so you can tune thresholds per category.

**Inline moderation of generated output.** Pass a top-level `moderation` object on a generation request and "the API returns moderation scores for the model input and generated output without a separate moderation request." If you are building on OpenAI's models already, that is convenient.

**Wide sample code.** The guide has examples for JavaScript, Python, Go, Java, C# and Ruby, plus raw HTTP.

**Honest about its limits.** The guide tells you not to treat scores as automatic decisions, and not to send child sexual abuse material. Vendors that say this plainly are easier to trust.

## Where it runs out

**No spam, scam or promotional category.** None of the 13 keys in the example response covers them. For community and marketplace moderation these are often the daily problem, and a safety classifier will not be built to flag them. (We would not describe this as a flaw. It is a different job.)

**Scores leave the decision to you.** OpenAI's own wording: "Treat moderation scores as signals for your application's policy, not as an automatic blocking decision." You choose and maintain thresholds.

**Not for child safety work.** "The API is not designed for CSAM detection or handling and is not a substitute for dedicated child-safety safeguards."

**Streaming caveat.** "If you stream a generated response, moderation scores arrive after the full generated output is available. They aren't included with partial output deltas." So you cannot use it to stop a stream part way.

**Refusals can be flagged.** "A refusal or other safety-aware response can still trigger a flag if it discusses harmful content." If you moderate your own assistant's replies, expect some flags on the assistant being careful.

**Audio is not classified, and video is not a listed input.** The guide states "It doesn't classify audio" and names text and images only.

## What the guide does not say

We looked and could not find these, so we are not claiming either way:

- Supported languages, or how it performs in them
- Rate limits for the moderation endpoint
- Latency
- Whether you can pass conversation history as context
- Which categories accept images versus text only (we did not read that table directly)

If any of these matter to you, test on your own data before committing.

## Where Supervisor differs

Supervisor is paid and, per message, often costs more than any free tool. In return it has 16 labels including spam, promotional, scam, self-harm and illegal, a `flagged` decision with `labels`, `include_context` (returns `needs_context` and `context_labels`), `implicit_labels`, video alongside text and images, translation of non-English messages before classification, three model tiers, a 50% discount on batches, a username endpoint, five SDKs and a Discord bot. Prices are in [OpenAI moderation pricing](/blog/openai-moderation-pricing) and the head to head is in [Supervisor vs OpenAI's moderation endpoint](/blog/supervisor-vs-openai-moderation).

## Verdict

Use OpenAI's endpoint if you are moderating your own application's inputs and outputs for the standard harm categories. Look at [alternatives](/blog/openai-moderation-alternatives) if you also need community-specific labels, decisions, context or video. Many teams sensibly use both.

Try your own messages in the [live demo](https://supervisor.gg/demo), read the [API docs](/docs/integrations/api), or [create a free account](https://supervisor.gg).

## Sources

- OpenAI, [Moderation guide](https://developers.openai.com/api/docs/guides/moderation)
- Supervisor, [API reference](/docs/integrations/api)
