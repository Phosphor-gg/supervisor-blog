---
title: "How to moderate messages in a chat app"
date: 2026-10-26
description: "Add automated moderation to a chat or messaging product: check each message before delivery, use conversation context for ambiguous replies, and clear a backlog with the batch endpoint."
---

# How to moderate messages in a chat app

**Bottom line:** check each message on your server before you deliver it, ask the API whether the message needs conversation context, and send the history only when it does. This guide builds that in Python with the Supervisor SDK.

## The problem

In a chat product, the worst messages are rarely the loudest. A word filter catches the obvious slur and misses the message that is cruel without a single flaggable word, the scam link with a friendly greeting, or "do it" sent to someone who has just said they feel awful. Meanwhile a strict filter blocks harmless banter and your users learn to work around it.

You need a classifier that returns reasons (labels), lets you choose which ones matter, and tells you when a message cannot be judged alone.

## 1. Set up

Sign up at [supervisor.gg](https://supervisor.gg), go to **Dashboard > API Keys** and create a key (it looks like `sk_prod_...`). Install the Python SDK from GitHub, it is not on PyPI:

```bash
pip install "git+https://github.com/Phosphor-gg/supervisor-sdk-python.git"
```

It requires Python 3.10 or later.

## 2. Moderate a message with context

```python
import os
from supervisor import SupervisorClient, ModerationModel, ModerationLabel

LABELS = [
    ModerationLabel.TOXICITY,
    ModerationLabel.HARASSMENT,
    ModerationLabel.HATE,
    ModerationLabel.INSULT,
    ModerationLabel.SEXUAL,
    ModerationLabel.SELF_HARM,
    ModerationLabel.SCAM,
    ModerationLabel.SPAM,
]

async def check_message(client, text, history):
    """history: earlier messages in the conversation, oldest first."""
    first = await client.moderate(
        text,
        model=ModerationModel.SENTINEL,
        enabled_labels=LABELS,
        include_context=True,
    )
    if first.flagged or not first.needs_context or not history:
        return first

    combined = "\n".join([*history, text])
    return await client.moderate(
        combined,
        model=ModerationModel.SENTINEL,
        enabled_labels=LABELS,
    )
```

How it works:

- `include_context=True` makes the response carry `needs_context` and `context_labels`. For `"stop it"` the API returns `flagged: false`, `needs_context: true` and `context_labels: ["harassment"]`.
- If the message is already flagged, you have your answer. If it does not need context, you also have your answer. Only the ambiguous case triggers a second request, with the recent history joined above the new message.
- `enabled_labels` limits the check to the labels your rules cover. Leave it out to check all 16.

Context-aware moderation is part of Premium, along with all three models.

Send only the messages that matter as history. The second request is billed by the size of the text you send, so a short window of recent lines costs less than a whole conversation.

## 3. Use it in your message handler

```python
import asyncio
from supervisor import SupervisorClient, SupervisorError

async def handle_incoming(client, conversation, sender, text):
    try:
        result = await check_message(client, text, conversation.recent_texts(10))
    except SupervisorError as e:
        if e.status_code == 402:
            alert_team("Supervisor credits exhausted")
        # Your policy: deliver unmoderated, or hold for review.
        return await conversation.hold_for_review(sender, text)

    if result.flagged:
        return await conversation.reject(sender, text, reasons=result.labels)
    return await conversation.deliver(sender, text)

async def main():
    async with SupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"]) as client:
        ...  # start your server and pass client to handlers
```

`conversation`, `alert_team` and the delivery methods are placeholders for your own code. The part that is the SDK's is the error handling: a failed request raises `SupervisorError`, whose `status_code` is `402` when your credits have run out. Requests keep failing with 402 until the monthly reset or an upgrade, so alert someone and decide, in advance, whether you deliver or hold in the meantime. The SDK also raises `RateLimitError` for `429`, `AuthenticationError` for `401` and `ValidationError` for `400`.

## 4. Check display names

```python
check = await client.check_username("user123")
if check.flagged:
    ...  # ask the user to pick another name
```

`check_username` returns `flagged` and a `score`.

## 5. Clear a backlog with the batch endpoint

If you are adding moderation to a product that already has messages, scan the existing ones with `moderate_batch`. It returns a list with one result per text, and batches of two or more are billed at 50% off.

```python
async def scan_backlog(client, messages):
    # The docs state no maximum batch size, so send chunks. 100 is our choice.
    for i in range(0, len(messages), 100):
        chunk = messages[i : i + 100]
        results = await client.moderate_batch(
            [m.text for m in chunk],
            model=ModerationModel.OBSERVER,
            enabled_labels=LABELS,
        )
        for m, r in zip(chunk, results):
            if r.flagged:
                print(m.id, r.labels)
```

Observer is the cheapest model, which suits a bulk pass. You can follow up on flagged items with a more accurate model.

## 6. Prefer synchronous code?

`SyncSupervisorClient` has the same methods without `await`:

```python
from supervisor import SyncSupervisorClient

with SyncSupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"]) as client:
    result = client.moderate("text to check")
    print(result.flagged, result.labels)
```

## Picking a model

All three models are included in Premium. Observer is roughly £0.0014 per KB of text, Sentinel (the default) roughly £0.0027 and Arbiter roughly £0.0055. A common split is Observer or Sentinel for the live path and Arbiter for anything a user appeals. Test with your own messages and decide.

## Summary

- Moderate before delivery, on the server.
- Scope with `enabled_labels`, ask for context with `include_context`.
- Send history only when `needs_context` is true.
- Handle `402` as a planned state.
- Use `moderate_batch` for backlogs.

Read the [API reference](/docs/integrations/api), try messages in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg) and get an API key.
