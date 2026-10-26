---
title: "OpenAI moderation endpoint pricing: free, and what Supervisor costs by comparison"
date: 2026-10-26
description: "OpenAI's moderation endpoint is free to use. Here is what that does and does not cover, what is not documented, and exactly what Supervisor costs per message so you can decide if paying is worth it."
---

# OpenAI moderation endpoint pricing: free, and what Supervisor costs by comparison

**Bottom line:** OpenAI's moderation endpoint is free to use, so it will always beat Supervisor on price. Supervisor is £13.99 a month for £120 of credits, which covers roughly 450,000 short text messages on the default model, and images cost far more than text. You pay Supervisor for what the free endpoint does not list, not for the same thing.

## What OpenAI charges

[OpenAI's moderation guide](https://developers.openai.com/api/docs/guides/moderation) says it directly: "The moderation endpoint is free to use, and image files can be up to 20 MB."

Two honest caveats from our reading:

- **The general pricing page has no moderation line.** We read OpenAI's [pricing page](https://platform.openai.com/docs/pricing) and it does not list a separate moderation price. The only statement that it is free is on the moderation guide itself.
- **Limits and account terms are not in the guide.** The guide does not mention rate limits for this endpoint, and does not say what kind of account you need. OpenAI's general [rate limits page](https://developers.openai.com/api/docs/guides/rate-limits) describes requests and tokens per minute in general terms and does not name a moderation figure in what we read. We did not read OpenAI's usage policies or terms of use, so check them before building a product on it.

We are not going to quote a requests-per-minute or per-day number for the endpoint, because we could not verify one. If volume matters, test it or ask OpenAI.

## What free means for your total cost

Free per request is not the same as free to run. Costs that stay with you:

- **Thresholds.** The endpoint returns scores, and OpenAI says to "treat moderation scores as signals for your application's policy, not as an automatic blocking decision." Someone has to choose and maintain the cut-offs.
- **Gaps you cover yourself.** The 13 categories in the guide's example response are a safety set. There is no spam, scam or promotional category in it, so those need another tool or your own rules.
- **Review time.** Whatever a free tool cannot decide ends up in a human queue.

For a lot of projects those costs are small and free is the right answer.

## What Supervisor costs

Supervisor is paid. Premium is the only plan on sale.

| Plan | Price | Monthly usage included |
|---|---|---|
| Premium, monthly | £13.99 | £120 of credits |
| Premium, yearly | £83.85 | £120 of credits a month |
| Premium, 3 years | £179.65 | £120 of credits a month |

New accounts get £0.25 of free credits to try it, usable for 7 days from your first moderated message. There is also a 7 day Premium trial, which needs a card (a £1 card check hold is released).

### Text

Text is billed by the byte, at a rate per model:

| Model | Relative cost | Approx. price per KB |
|---|---|---|
| Observer | 1x | £0.0014 |
| Sentinel (default) | 2x | £0.0027 |
| Arbiter | 4x | £0.0055 |

Worked example (our arithmetic): a 100 byte message on Sentinel costs about £0.00027. £120 of credits covers about 450,000 of those a month. On Observer it is about 900,000, and on Arbiter about 225,000. Batches of two or more are billed at half price.

A 1,000 byte message on Sentinel costs about £0.0027, so the same allowance covers about 45,000. Cost scales with length, so long messages are where Supervisor gets expensive relative to anything priced per request.

### Images and video

Images are the costly part. They are billed at about £0.0014 per KB regardless of model, so a 100 KB image is roughly £0.14. The monthly allowance covers a little under 900 images of that size. If the image has readable text, that text is billed on top at the text rate. Video frames are billed at a quarter of the image rate, and a clip analyses at most 20 frames.

Repeating an identical request inside the cache window consumes no credits. When credits run out, requests fail with `402 Payment Required` until they reset.

## What the extra money buys

- 16 labels including spam, promotional, scam, self-harm and illegal
- A `flagged` decision plus `labels`, instead of scores only
- `include_context`, which returns `needs_context` and `context_labels`
- `implicit_labels` for harm that is not stated outright
- Video as well as text and images, in one API
- Translation of non-English messages before classification
- A username check endpoint, SDKs in five languages, and a Discord bot

Whether that is worth it depends on whether you need any of it. We do not know your content, and we are not going to pretend a free endpoint is the wrong choice when it may be exactly right.

## A sensible way to decide

1. Run your real messages through OpenAI's endpoint and see what it misses.
2. Run the misses through the [live demo](https://supervisor.gg/demo).
3. Only pay if the gap is worth £13.99 a month to you.

Compare the surfaces in the [API docs](/docs/integrations/api), or [create a free account](https://supervisor.gg) and use the free credits. For the full feature comparison see [Supervisor vs OpenAI's moderation endpoint](/blog/supervisor-vs-openai-moderation).

## Sources

- OpenAI, [Moderation guide](https://developers.openai.com/api/docs/guides/moderation)
- OpenAI, [Pricing](https://platform.openai.com/docs/pricing) and [Rate limits](https://developers.openai.com/api/docs/guides/rate-limits)
- Supervisor, [API reference: credits and billing](/docs/integrations/api)
