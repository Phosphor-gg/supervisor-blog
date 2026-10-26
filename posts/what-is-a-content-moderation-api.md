---
title: "What is a content moderation API?"
date: 2026-10-26
description: "A content moderation API classifies user-generated text, images and video and tells your software what is wrong with it. Here is what one does, what a request looks like, and what it leaves for you to build."
---

# What is a content moderation API?

**Bottom line:** a content moderation API takes something a user wrote or uploaded, and returns a verdict and reasons that your own code acts on. It does the classification. You keep the decisions: what to hide, whom to warn, what a moderator sees.

## The problem it solves

Any product where users create content, whether chat, comments, listings, profiles or uploads, ends up with content you do not want. Reviewing it by hand does not scale, and writing rules by hand does not keep up. A moderation API replaces the "is this acceptable?" step with a function call, so the rest of your system can stay ordinary code.

The [glossary entry](/glossary/content-moderation-api) has the short definition. This post covers how it works in practice, using Supervisor as the example.

## The anatomy of a call

You send content to an endpoint with an API key. You get back a decision and the categories (labels) behind it.

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Your content to moderate",
    "model": "sentinel"
  }'
```

```json
{
    "flagged": true,
    "labels": ["toxicity", "insult"],
    "model_version": "2.1"
}
```

Your code reads `flagged`, and may read `labels`:

```python
result = client.moderate("text to check")
if result.flagged:
    hide_and_log(result.labels)
```

(`client` here is the [Python SDK](/docs/sdks/python) client, and `hide_and_log` is yours.)

## What it can look at

- **Text:** chat messages, comments, posts, listings, names.
- **Images:** sent as base64 to the same endpoint.
- **Video:** short clips, with a verdict per analysed frame and timestamps.
- **Usernames:** a separate endpoint that returns a flag and a score.

Different APIs support different mixes of these, so check this before you choose one.

## What it returns

The useful ideas, using Supervisor's names:

- **Labels.** Categories such as profanity, toxicity, harassment, hate, insult, sexual, violence, self-harm, spam, promotional, scam and illegal. Supervisor has 16 (see [moderation labels](/glossary/moderation-labels)). You can restrict a call to the labels your rules cover with `enabled_labels`.
- **A decision.** `flagged` is true when any enabled label fires, so you do not have to pick a numeric threshold per category.
- **Context signals.** With `include_context`, the response can say `needs_context` and name `context_labels`, meaning "this might be a problem, but I need the surrounding conversation". Then you send the history in a second request.
- **Implicit harm.** `implicit_labels` for content that is harmful without saying so outright (a plan feature; included in Premium). See [implicit moderation](/glossary/implicit-moderation).

## How you pay

Moderation APIs usually bill by usage. Supervisor bills by size: text by the byte at the chosen model's rate, images by file size. The rates are roughly £0.0014 per KB on Observer, £0.0027 on Sentinel (the default) and £0.0055 on Arbiter. Premium is £13.99 a month with £120 of credits included, and batches of two or more texts are half price. When credits run out, requests fail with `402 Payment Required` until the monthly reset or an upgrade.

## What an API does not do

This is the part people underestimate.

- **It does not enforce.** It does not delete, ban or warn. You write that.
- **It does not know your rules.** Labels are general categories. Whether `promotional` is a violation on your platform is your decision.
- **It is not infallible.** Any classifier produces [false positives](/glossary/false-positive) and misses. Keep a path for users to appeal and for moderators to review.
- **It is not a moderation team.** For anything serious, route flagged content to humans with the labels attached.

## Typical integration patterns

1. **Pre-publish check.** Moderate before the content is visible, then publish, hold or reject.
2. **Post-publish sweep.** Publish immediately and moderate asynchronously, hiding after the fact. Easier on latency, but harm is visible meanwhile.
3. **Backlog scan.** Run existing content through the batch endpoint when you first adopt moderation.
4. **Report triage.** Use labels to prioritise what moderators see first.

Worked examples: [in-game chat](/blog/moderate-in-game-chat), [chat apps](/blog/moderate-chat-app-messages), [comments](/blog/moderate-comments-section), [marketplace listings](/blog/moderate-marketplace-listings) and [forums](/blog/moderate-forum-posts).

## Choosing one

Questions to ask of any moderation API:

- Which content types does it cover: text, images, video, usernames?
- Can you scope categories to your rules?
- Can it say when a message needs context?
- How is it priced, and can you predict your bill?
- What happens when you run out of credits or it is unreachable?
- Do you need to build something yourself instead? See [build vs buy](/blog/build-vs-buy-content-moderation).

## Summary

- A moderation API classifies content and returns a decision plus reasons.
- You still own enforcement, rules and review.
- Look at content types, label scope, context handling and pricing.

Read the [API reference](/docs/integrations/api), try messages in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg) and get an API key.
