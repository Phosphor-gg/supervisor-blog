---
title: "How to detect toxicity in Python"
date: 2026-10-26
description: "Detect toxic, abusive and spammy text in Python with the Supervisor SDK: install, async and sync clients, label filtering, context, batches and error handling."
---

# How to detect toxicity in Python

**Bottom line:** install the Supervisor SDK from GitHub, create a client with your API key, and call `moderate()`. You get back `flagged` and the list of labels that fired, and you decide what to do. This guide covers the sync and async clients, scoping labels, context, batches and errors.

## The problem

Toxicity detection in Python usually starts with a regex or a banned word list, and ends with a rewrite once people find the gaps. A classifier API gives you one call that returns a decision and reasons, so your code stays small.

## Install

The SDK is installed from GitHub, not PyPI:

```bash
pip install "git+https://github.com/Phosphor-gg/supervisor-sdk-python.git"
```

Or with [uv](https://docs.astral.sh/uv/):

```bash
uv pip install "git+https://github.com/Phosphor-gg/supervisor-sdk-python.git"
```

It requires Python 3.10 or later. Get an API key from **Dashboard > API Keys** after signing up at [supervisor.gg](https://supervisor.gg). Keys look like `sk_prod_...`.

## Your first check

```python
import asyncio
import os
from supervisor import SupervisorClient

async def main():
    async with SupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"]) as client:
        result = await client.moderate("text to check")
        print(result.flagged, result.labels)

asyncio.run(main())
```

Prefer synchronous code? `SyncSupervisorClient` has the same methods without `await`:

```python
from supervisor import SyncSupervisorClient

with SyncSupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"]) as client:
    result = client.moderate("text to check")
```

A `ModerationResponse` has `flagged`, `labels`, `implicit_labels`, `model_version`, and optional context fields (`needs_context`, `context_labels`). When content is flagged, `labels` lists the categories, for example `["toxicity", "insult"]`.

## Toxicity is one of 16 labels

`toxicity` is general toxicity. The full set is profanity, toxicity, harassment, hate, insult, sexual, sexual/unlawful, sexual/explicit, sensitive, violence, self-harm, medical, spam, promotional, scam and illegal. Call `get_labels()` to list them with descriptions.

To check only the ones you care about, pass `enabled_labels`:

```python
from supervisor import ModerationLabel, ModerationModel

result = client.moderate(
    "text to check",
    model=ModerationModel.SENTINEL,
    enabled_labels=[
        ModerationLabel.TOXICITY,
        ModerationLabel.INSULT,
        ModerationLabel.HARASSMENT,
        ModerationLabel.HATE,
    ],
)
```

There are three models: Observer (roughly £0.0014 per KB), Sentinel, the default (roughly £0.0027 per KB) and Arbiter (roughly £0.0055 per KB). Pass `model=` to choose.

## There is no score to threshold

Some toxicity APIs return a number per attribute and leave you to pick a cut-off. Supervisor returns `flagged` and `labels`, so the usual code is:

```python
if result.flagged:
    reject(result.labels)
```

If you need a middle ground, use `implicit_labels` (content that is harmful without saying so outright, returned on plans that include implicit moderation, which Premium does) as a "send to review" signal.

## Short replies: use context

```python
first = client.moderate("stop it", include_context=True)
# flagged=False, needs_context=True, context_labels=["harassment"]
if not first.flagged and first.needs_context:
    full = client.moderate("\n".join(history + ["stop it"]))
```

If `needs_context` is true, send the message history in a follow-up request. Joining the earlier messages above the new one is how Supervisor's Discord bot does it. Context-aware moderation is included with Premium.

## Batches

```python
results = client.moderate_batch(
    ["First message", "Second message", "Third message"],
    model=ModerationModel.OBSERVER,
)
for r in results:
    print(r.flagged, r.labels)
```

You get a list of `ModerationResponse`, one per text. Batches of two or more are billed at 50% off, so use them for backlogs and nightly jobs. The docs state no maximum batch size, so chunk large jobs.

## Errors

```python
from supervisor import (
    SupervisorError, AuthenticationError, RateLimitError, ValidationError,
)

try:
    result = client.moderate("text to check")
except AuthenticationError:
    ...  # 401: bad or missing key
except RateLimitError:
    ...  # 429: back off and retry later
except ValidationError:
    ...  # 400 or 422: bad request, or a model your plan does not include
except SupervisorError as e:
    if e.status_code == 402:
        ...  # credits exhausted until the monthly reset or an upgrade
    else:
        raise
```

`402 Payment Required` has no dedicated exception class; it arrives as a plain `SupervisorError` with `status_code == 402`.

## Other media and checks

- Images: `client.moderate(image=base64_string)`. See [moderating user-uploaded images](/blog/moderate-user-uploaded-images).
- Videos: `client.moderate_video("clip.mp4")`. See [moderating user-uploaded videos](/blog/moderate-user-uploaded-videos).
- Usernames: `client.check_username("user123")` returns `flagged` and `score`.

## Summary

- `pip install` from GitHub, then `moderate()`.
- Read `flagged` and `labels`, no threshold needed.
- Scope with `enabled_labels`, add `include_context` for short replies.
- Use `moderate_batch` for volume.
- Treat `402` as credits exhausted.

See the [Python SDK docs](/docs/sdks/python) and [API reference](/docs/integrations/api), try the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
