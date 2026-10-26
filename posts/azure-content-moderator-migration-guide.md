---
title: "Azure Content Moderator is retiring on 15 March 2027: how to migrate"
date: 2026-10-26
description: "Microsoft is retiring Azure Content Moderator on 15 March 2027 and points users to Azure AI Content Safety. Here is what the notice says, what to check in a replacement, and how to move your checks to Supervisor step by step."
---

# Azure Content Moderator is retiring on 15 March 2027: how to migrate

**Bottom line:** Microsoft says Azure Content Moderator "is deprecated as of February 2024 and will be retired on March 15, 2027." If your product calls it, you need a replacement live before then. Microsoft's own answer is Azure AI Content Safety. This guide covers what the notice says, what to look for in a replacement, and how to move to Supervisor if Content Safety is not the right fit. Supervisor is paid and does not replace every Content Moderator feature, and we say which below.

## What Microsoft has announced

The [Content Moderator overview](https://learn.microsoft.com/en-us/azure/ai-services/content-moderator/overview) says: "Azure Content Moderator is deprecated as of February 2024 and will be retired on March 15, 2027. It is replaced by Azure AI Content Safety, which offers advanced AI features and enhanced performance."

The same page lists what Content Moderator offers: text moderation, custom term lists, image moderation, custom image lists, and video moderation. Work out which of those you actually use, because that decides which replacement fits.

## Do not leave it to the last month

1. **Thresholds need retuning.** Every model scores differently. Whatever cut-offs you chose will not carry over, so run old and new side by side for a few weeks.
2. **Lists and rules need rebuilding.** Custom term lists and image lists do not move automatically. Plan the time.

## What to look for in a replacement

- **Which of your features it covers.** Text, images, video, custom lists. Check each against the replacement's docs, not a summary.
- **Categories you need.** Azure AI Content Safety has four built-in categories (hate, sexual, violence, self-harm). If you also moderate spam, scams or promotion, check how you would cover that.
- **Languages.** Check how slang and mixed-language messages are handled.
- **Pricing you can predict.** Work out a monthly bill from your volume. Our [Azure pricing breakdown](/blog/azure-content-safety-pricing) shows how per-record and per-byte pricing differ.

## Your options

**Azure AI Content Safety** is Microsoft's stated replacement. It has text and image APIs, severity levels, blocklists (the closest feature we found to custom term lists, so confirm the fit in Microsoft's docs), and a free tier. In the pages we read, we did not find video input, so if you use Content Moderator's video moderation, check Microsoft's API reference and migration guidance. See our [review](/blog/azure-content-safety-review).

**Supervisor** moves you off Azure entirely. Honest differences first:

- It is a paid service with no standing free tier. For longer text and for images it costs noticeably more than Azure's list prices (images especially).
- We could not find a custom term list or custom image list feature in the Supervisor API docs. If you rely on those, keep that logic in your own code or choose a service that has it.

What you get for the cost:

| | Supervisor |
|---|---|
| Labels | 16: profanity, toxicity, harassment, hate, insult, sexual, sexual (unlawful), sexual (explicit), sensitive, violence, self-harm, medical, spam, promotional, scam, illegal |
| Context | `include_context` tells you when a message needs conversation history, and which labels it might fall under |
| Implicit harm | `implicit_labels` for content that is harmful without saying so outright |
| Media | Text, images and short videos (up to 60 seconds, 10 MB) in the same API |
| Languages | Non-English messages are translated before they are classified, including slang and mixed-language messages |
| Models | Observer (fastest, cheapest), Sentinel (default), Arbiter (most accurate) |
| Volume | Batch endpoint, batches of two or more billed at half price |
| Extras | Username check endpoint, SDKs for Python, JavaScript, Go, Rust and Java, a ready-made Discord bot |

Premium is £13.99 a month with 90,000,000 credits. A 100 byte message on Sentinel is 200 credits, so the allowance covers about 450,000 messages that size (900,000 on Observer). Images are billed per byte, roughly £0.14 for 100 KB. New accounts get free credits to test with (Observer model, text only), and there is a 7 day Premium trial.

## How to migrate to Supervisor, step by step

### 1. Get an API key

Sign up at [supervisor.gg](https://supervisor.gg) with Discord, Google or GitHub, then go to **Dashboard > API Keys** and create a key. Keys look like `sk_prod_...`.

### 2. Replace the Content Moderator call

Supervisor returns a decision: `flagged`, plus the labels that triggered it.

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

```json
{
    "text": "Your content to moderate",
    "enabled_labels": ["toxicity", "insult", "harassment", "hate"]
}
```

Start with the scope you had, then switch on `spam`, `scam` and the rest once you have seen what they catch.

### 4. Images and video

Send base64 image data in the `image` field (text and images go in separate requests). Videos go to `POST /api/moderation/user/video` and come back with per-frame results, or use `client.moderate_video("clip.mp4")` in the Python SDK. Limits: 10 MB and 60 seconds.

### 5. Turn on context where it matters

```json
{
    "text": "stop it",
    "include_context": true
}
```

If the response has `needs_context: true`, send the message again with its recent history.

### 6. Rebuild your lists in your own code

For custom term lists, a simple pre-check in your application before calling the API works, and it also saves credits on messages you were going to block anyway.

### 7. Move bulk jobs to the batch endpoint

Use `POST /api/batch` with a `texts` array. Batches of two or more cost half as much per message.

### 8. Run both until you trust it

Until 15 March 2027, call both services, log where they disagree and read those messages. That tells you more than any comparison table, including this one.

## Summary

- Azure Content Moderator is retired on 15 March 2027, per Microsoft.
- Microsoft's stated replacement is Azure AI Content Safety. Check it covers the features you use, especially video and custom lists.
- Supervisor covers 16 labels, context, images and video in one API, at £13.99 a month for 90 million credits. It costs more than Azure for longer text and images and has no documented custom lists.
- Plan time for retuning thresholds and rebuilding lists.

Read the [API reference](/docs/integrations/api), try messages in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg) and get an API key. Comparison: [Supervisor vs Azure AI Content Safety](/blog/supervisor-vs-azure-content-safety).

## Sources

- Microsoft, [Content Moderator overview](https://learn.microsoft.com/en-us/azure/ai-services/content-moderator/overview)
- Microsoft, [Content Safety overview](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview) and [text quickstart](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/quickstart-text)
- Supervisor, [API reference](/docs/integrations/api)
