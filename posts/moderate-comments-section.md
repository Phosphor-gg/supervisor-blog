---
title: "How to moderate a comments section automatically"
date: 2026-10-26
description: "Stop spam, scams and abuse in blog, video or app comments: moderate on submit, hold borderline comments for review, and clean up an existing comment backlog in bulk."
---

# How to moderate a comments section automatically

**Bottom line:** moderate every comment when it is submitted, publish what passes, and hold what is flagged for a human. Use the batch endpoint to clean up the comments you already have. This guide uses Python and the Supervisor SDK.

## The problem

Open comments attract three kinds of trouble: abuse aimed at other commenters, spam and promotional links, and scams that look like friendly replies. Manual review does not scale, and a banned word list only catches the first kind, and only when it is spelled the way you expected.

Comments also differ from chat in one useful way: you rarely need to decide in milliseconds. You can hold a comment for a moment, or publish it as pending, which lets you be more careful.

## 1. Set up

Create an account at [supervisor.gg](https://supervisor.gg), make a key under **Dashboard > API Keys** (`sk_prod_...`), and install the SDK:

```bash
pip install "git+https://github.com/Phosphor-gg/supervisor-sdk-python.git"
```

## 2. Decide what each label means for you

Supervisor has 16 labels. For comments, a sensible starting map:

| Label | Typical action |
| --- | --- |
| `spam`, `promotional`, `scam` | Hold or reject |
| `hate`, `harassment`, `insult`, `toxicity` | Hold for review |
| `sexual`, `sexual/explicit`, `sexual/unlawful` | Reject |
| `profanity` | Your call: many sites allow it |
| `illegal`, `self-harm`, `violence` | Hold and review quickly |

This table is a starting point, not a rule. The point is that the API reports which labels fired, so the action is yours.

## 3. Moderate on submit

```python
import os
from supervisor import SyncSupervisorClient, ModerationModel, ModerationLabel, SupervisorError

REJECT = {"sexual", "sexual/explicit", "sexual/unlawful", "scam", "spam"}

client = SyncSupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"])

def review_comment(text: str) -> str:
    """Returns 'publish', 'hold' or 'reject'."""
    try:
        result = client.moderate(text, model=ModerationModel.SENTINEL)
    except SupervisorError as e:
        if e.status_code == 402:
            notify_admin("Moderation credits have run out")
        return "hold"  # fail safe: nothing publishes unreviewed

    if not result.flagged:
        return "publish"
    if REJECT & set(result.labels):
        return "reject"
    return "hold"
```

`notify_admin` is your own function. Returning `hold` on any error means a moderation outage delays comments rather than letting everything through. When credits run out the API returns `402 Payment Required` until the monthly reset or an upgrade, so this path is worth testing.

The response also has `implicit_labels` for content that is harmful without saying so outright. On plans that include implicit moderation (Premium does), these arrive in the same response with no extra parameter. A comment can pass the explicit labels and still carry an implicit one, so treat a non-empty `implicit_labels` as a reason to hold:

```python
    if result.implicit_labels:
        return "hold"
```

Put that check after the `flagged` branch if you want flagged comments to follow your reject rules first.

## 4. Replies need context

A reply of "you again?" is hard to judge alone. Ask for context and, when the API says it needs it, send the parent comment with the reply:

```python
def review_reply(text: str, parent_text: str) -> str:
    first = client.moderate(text, include_context=True)
    if first.flagged:
        return "hold"
    if first.needs_context:
        second = client.moderate(f"{parent_text}\n{text}")
        return "hold" if second.flagged else "publish"
    return "publish"
```

Joining the earlier text first and the new text last is how Supervisor's own Discord bot builds its follow-up request. Context-aware moderation is included with Premium.

## 5. Clean up the comments you already have

Run your existing comments through the batch endpoint once. It returns one result per text, and a batch of two or more texts is billed at 50% off:

```python
def scan_existing(comments):
    # No maximum batch size is documented, so send chunks. 100 is our choice.
    for i in range(0, len(comments), 100):
        chunk = comments[i : i + 100]
        results = client.moderate_batch(
            [c["body"] for c in chunk],
            model=ModerationModel.OBSERVER,
            enabled_labels=[
                ModerationLabel.SPAM,
                ModerationLabel.PROMOTIONAL,
                ModerationLabel.SCAM,
                ModerationLabel.HATE,
                ModerationLabel.HARASSMENT,
            ],
        )
        for c, r in zip(chunk, results):
            if r.flagged:
                queue_for_review(c["id"], r.labels)
```

Repeating an identical request within the cache window consumes no credits, so re-running a scan over unchanged text is not charged twice, per the credits section of the API reference.

## 6. Show moderators why

Store `labels` with each held comment. A review queue that says "held: scam" is far quicker to work through than one that only says "flagged".

## Summary

- Moderate on submit and map labels to publish, hold or reject.
- Fail to `hold`, and handle `402`.
- Use `include_context` for replies.
- Use `moderate_batch` for existing comments.

Read the [API reference](/docs/integrations/api), paste real comments into the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg).
