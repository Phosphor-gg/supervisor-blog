---
title: "Perspective API is shutting down: how to migrate before 31 December 2026"
date: 2026-10-26
description: "Google Jigsaw is ending Perspective API after 2026 with no migration support. Here is what the shutdown means, what to look for in a replacement, and how to move your toxicity checks to Supervisor step by step."
---

# Perspective API is shutting down: how to migrate before 31 December 2026

**Bottom line:** Perspective API stops working after 31 December 2026, and Google Jigsaw is not offering migration help. If your product calls it, you need a replacement live before then. This guide covers what changes, what to look for in a new API, and how to move to Supervisor in an afternoon.

## What Jigsaw has announced

The notice on [perspectiveapi.com](https://www.perspectiveapi.com/) is short and final:

- "Perspective API is sunsetting and service is officially ending after 2026."
- "The service will remain active until December 31, 2026."
- "We will not be offering direct migration support."
- Usage and quota increase requests were only accepted until February 2026, so if you are near your quota now, you cannot get more.
- There is no extension: "The API will no longer be in service after 2026."

Jigsaw's stated reason is that "AI capabilities have evolved, and there is now less demand for a standalone tool specific to this area."

Perspective did a lot for online conversations, and plenty of products were built on it. The point of this post is not that it was bad. It is that it is going away, and your moderation should not go away with it.

## Do not leave it to the last week

Two practical reasons to move now rather than on 30 December:

1. **Thresholds need retuning.** Every model scores differently. Whatever cut-off you picked for Perspective will not carry over, so you want a few weeks of running both side by side.
2. **Holiday traffic.** For most communities and games, late December is busy. That is the worst time to be swapping a safety system.

## What to look for in a replacement

Perspective scored a comment for attributes such as `TOXICITY`. Its own model card says it "is not intended to be used for fully automated moderation", and that the toxicity model only looks at an individual statement. Those limits are worth fixing while you are migrating anyway. When you compare replacements, check:

- **More than toxicity.** Scams, spam, self-promotion and sexual content are often a bigger problem than rudeness.
- **Conversation context.** "Stop it" means nothing on its own. A replacement should be able to tell you when a message needs the surrounding conversation to judge.
- **Images and video.** If users can post media, a text-only API leaves a gap.
- **Languages.** Check that slang and mixed-language messages are handled, not just clean textbook text.
- **Clear pricing you can predict.** You should be able to work out your monthly bill from your message volume.

## Why Supervisor

Supervisor is a moderation API built for communities, games and platforms. It is a paid service, so if you were on Perspective for free this is a cost increase. Here is what you get for it.

| | Supervisor |
|---|---|
| Labels | 16: profanity, toxicity, harassment, hate, insult, sexual, sexual (unlawful), sexual (explicit), sensitive, violence, self-harm, medical, spam, promotional, scam, illegal |
| Context | `include_context` tells you when a message needs conversation history, and which labels it might fall under |
| Implicit harm | `implicit_labels` for content that is harmful without saying so outright |
| Media | Text, images and short videos (up to 60 seconds, 10 MB) through the same API |
| Languages | Non-English messages are translated before they are classified, including slang and mixed-language messages |
| Models | Three: Observer (fastest, cheapest), Sentinel (default), Arbiter (most accurate) |
| Volume | A batch endpoint, with batches of two or more billed at half price |
| Extras | A username check endpoint, SDKs for Python, JavaScript, Go, Rust and Java, and a ready-made Discord bot |

### What it costs

Premium is £13.99 a month and includes 90,000,000 credits, all three models, context, image and video moderation. Text is billed by size: roughly £0.0014 per KB on Observer, £0.0027 per KB on Sentinel and £0.0055 per KB on Arbiter.

As a worked example, a 100 byte message on Sentinel costs 200 credits, so the monthly allowance covers about 450,000 messages that size. On Observer it is about 900,000, and batching halves the cost again. New accounts get free credits to test with (Observer model, text only), and there is a 7 day Premium trial.

## How to migrate, step by step

### 1. Get an API key

Sign up at [supervisor.gg](https://supervisor.gg) with Discord, Google or GitHub, then go to **Dashboard > API Keys** and create a key. Keys look like `sk_prod_...`.

### 2. Replace the Perspective call

Perspective returns a score per attribute and leaves the decision to you. Supervisor returns the decision: `flagged`, plus the labels that triggered it.

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

So wherever your code did `if toxicity_score > threshold`, it now reads `flagged`, or checks `labels` for the categories you care about.

In Python, using the [official SDK](/docs/sdks/python):

```bash
pip install "git+https://github.com/Phosphor-gg/supervisor-sdk-python.git"
```

```python
from supervisor import SyncSupervisorClient

with SyncSupervisorClient(api_key="sk_prod_...") as client:
    result = client.moderate("text to check")
    if result.flagged:
        print("Blocked for:", result.labels)
```

There are SDKs for [JavaScript](/docs/sdks/javascript), [Go](/docs/sdks/go), [Rust](/docs/sdks/rust) and [Java](/docs/sdks/java) too.

### 3. Choose which labels count

If you only used Perspective for toxicity and want to keep the same scope at first, pass `enabled_labels`:

```json
{
    "text": "Your content to moderate",
    "enabled_labels": ["toxicity", "insult", "harassment", "hate"]
}
```

Then switch on `spam`, `scam` and the rest once you have seen what they catch.

### 4. Turn on context where it matters

```json
{
    "text": "stop it",
    "include_context": true
}
```

If the response has `needs_context: true`, send the message again with its recent history for a proper decision. This is the case Perspective's single-statement design could not handle.

### 5. Move bulk jobs to the batch endpoint

If you were scoring backlogs or comment dumps, use `POST /api/batch` with a `texts` array. Batches of two or more cost half as much per message.

### 6. Run both until you trust it

Until 31 December, call both APIs, log where they disagree, and look at those messages. That tells you more about the replacement than any comparison table, including this one.

## Summary

- Perspective API ends after 31 December 2026, with no extension and no migration support.
- Move now so you have time to tune, not during the holiday rush.
- Supervisor covers 16 labels, conversation context, images and video in one API, at £13.99 a month for 90 million credits.
- Migrating is mostly swapping a score threshold for a `flagged` check.

Read the [API reference](/docs/integrations/api), try messages in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg) and get an API key.
