---
title: "How to moderate multilingual content without per-language word lists"
date: 2026-10-26
description: "Supervisor translates non-English text to English before classifying it, so one set of labels applies across the languages your users write in. Here is how that works and how to test it on your own content."
---

# How to moderate multilingual content without per-language word lists

**Bottom line:** if your users write in more than one language, you do not need a moderation list per language. Supervisor translates non-English text to English before it classifies it, so you call the same endpoint with the same labels whatever the language. This guide explains how that works, what to test, and how to wire it up.

## The problem

Every language multiplies the work of a list-based filter. One banned term becomes a list per language, each with its own spelling variants, and a user can switch language to get past a filter tuned for another. Messages that mix languages in one sentence are worse.

## How it works

Supervisor's moderation pipeline translates non-English text to English before classifying it. You do not tell the API what language the text is in, and there is no parameter to set. You send the text as the user wrote it:

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Your content to moderate, in any language",
    "model": "sentinel"
  }'
```

The response is the same as for English: `flagged`, `labels`, `model_version`.

We are not publishing a language count. This is a translation based approach, so how well it works in a given language depends on how well the text translates. The responsible way to know is to test on your own content, which is what the rest of this guide helps with.

## 1. Set up

Sign up at [supervisor.gg](https://supervisor.gg), create a key under **Dashboard > API Keys** (`sk_prod_...`), and install the SDK:

```bash
pip install "git+https://github.com/Phosphor-gg/supervisor-sdk-python.git"
```

## 2. Build a test set from your own users

Take a sample of real messages in each language you care about, including some you know are fine and some you know should be flagged. Label them yourself or with your moderators. A few dozen per language is enough to see obvious problems; it is not enough for statistics, so do not quote a rate from it.

```python
import os
from supervisor import SyncSupervisorClient

samples = [
    # (language, text, should_flag) - fill with your own messages
    ("fr", "...", False),
    ("es", "...", True),
    ("de", "...", False),
]

with SyncSupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"]) as client:
    results = client.moderate_batch([text for _, text, _ in samples])

for (lang, text, expected), r in zip(samples, results):
    if r.flagged != expected:
        print(f"MISMATCH [{lang}] expected={expected} labels={r.labels}: {text}")
```

`moderate_batch` returns one result per text, and batches of two or more cost half as much, which makes it the cheapest way to run an evaluation. Read the mismatches. Some will be your labelling, some will be places where you want a different model or a different set of enabled labels.

## 3. Configure once

Because the classification happens after translation, configuration is the same everywhere:

```python
from supervisor import ModerationLabel, ModerationModel

result = client.moderate(
    user_text,
    model=ModerationModel.SENTINEL,
    enabled_labels=[
        ModerationLabel.HARASSMENT,
        ModerationLabel.HATE,
        ModerationLabel.SCAM,
        ModerationLabel.SPAM,
    ],
)
```

One label set, one threshold for what you act on, whatever the language.

## 4. Use context for short replies

A short reply is ambiguous in any language. Use `include_context=True` and, when `needs_context` comes back true, send the previous messages with it:

```python
first = client.moderate(text, include_context=True)
if not first.flagged and first.needs_context:
    full = client.moderate("\n".join(history + [text]))
```

Context-aware moderation is included with Premium.

## 5. Pick a model for the hard languages

If the test set shows weak spots, try the same set on Arbiter, the most accurate model (roughly £0.0055 per KB against roughly £0.0027 on Sentinel and £0.0014 on Observer), or use it only for items your first pass flags or finds ambiguous. All three models are included in Premium, so this is a cost decision, not an access one.

## 6. Keep humans for the edges

Translation can lose tone, and so can any classifier. For communities where a misjudgement matters, route flagged items to a moderator with the original text and labels, rather than acting automatically. See the glossary on [false positives](/glossary/false-positive).

## What this does not solve

- Your rules still decide what is acceptable. A joke in one culture may be an insult in another, and `enabled_labels` is the only dial the API gives you.
- An English-only moderator team still cannot read the original. Show them the original and the labels, and expect to hire or consult for the languages your community is large in.

## Summary

- Send text in whatever language the user wrote, with no language parameter.
- Non-English text is translated to English before classification.
- Test with your own samples and use `moderate_batch` to do it cheaply.
- Configure labels once, and use context and Arbiter where the test shows a need.

Read the [API reference](/docs/integrations/api), try a message in your own language in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
