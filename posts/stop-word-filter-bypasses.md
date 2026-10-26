---
title: "How to stop word filter bypasses: l33t-speak, homoglyphs and spaced letters"
date: 2026-10-26
description: "Why word lists fail against character substitution, zero-width characters and spacing, and how to test your own filter against those tricks and move to a classifier that reads meaning."
---

# How to stop word filter bypasses: l33t-speak, homoglyphs and spaced letters

**Bottom line:** a word list matches strings, and bypassing it only needs the string to change. You can chase variants forever, or you can classify what the message means. This guide shows the common bypasses, a script that tests your filter against them, and how to call Supervisor instead.

## The problem

You add a word to the list. Within a day someone types it with a number in place of a letter. You add that. Next they use a lookalike character from another alphabet, or put a space between every letter, or hide invisible characters inside the word. Each fix handles one trick and invites the next, and meanwhile your list grows, your false positives grow with it, and the people you wanted to stop barely slow down.

For a short overview of the same problem on our site, see [the word filter bypass page](/word-filter-bypass).

## The usual bypasses

| Trick | What it looks like | Why a list misses it |
| --- | --- | --- |
| Character substitution (l33t-speak) | `1d10t` for `idiot` | Different characters, so no string match |
| Unicode homoglyphs | Cyrillic `і` in place of Latin `i` | Looks identical to a person, different code point |
| Zero-width characters | Invisible characters between letters | The word is split in the raw string |
| Spaced out letters | `i d i o t` | A space breaks the match |
| Misspelling and elongation | `iiidiot` | Not in the list unless you added it |

The first four are mechanical, which means you can test for them.

## Test your own filter

This script builds variants of a test word and runs them through a basic word-list check and through Supervisor. It uses a mild word on purpose. Replace it with terms from your own rules.

```python
import os
from supervisor import SyncSupervisorClient, ModerationLabel

WORD = "idiot"
BANNED = {"idiot"}  # stand-in for your current word list

variants = {
    "plain": "you are an idiot",
    "l33t": "you are an 1d10t",
    "homoglyph": "you are an іdіot",  # Cyrillic i
    "zero-width": "you are an i​d​i​o​t",
    "spaced": "you are an i d i o t",
}

def word_list_flags(text: str) -> bool:
    return any(word in text.lower() for word in BANNED)

with SyncSupervisorClient(api_key=os.environ["SUPERVISOR_API_KEY"]) as client:
    print(f"{'variant':<12}{'word list':<12}{'supervisor':<12}labels")
    for name, text in variants.items():
        result = client.moderate(text, enabled_labels=[ModerationLabel.INSULT, ModerationLabel.TOXICITY])
        print(f"{name:<12}{str(word_list_flags(text)):<12}{str(result.flagged):<12}{result.labels}")
```

Run it with your own words and your own samples and read the table. We are not quoting a catch rate here, and a handful of examples proves nothing statistically anyway. What the script gives you is something better for your situation: evidence on the messages that matter to your community.

You can also paste variants into the [live demo](https://supervisor.gg/demo) without writing code.

## Why a classifier handles this differently

Supervisor reads what a message means and returns labels, rather than matching strings against a list. There is nothing to add to when someone finds a new spelling. That is the design; how well it holds on your content is what the test above is for.

The practical consequences:

- **No list to maintain.** You choose labels (`profanity`, `toxicity`, `insult`, `harassment`, `hate` and 11 more) rather than words.
- **Scope with `enabled_labels`.** Turn on the categories your rules cover.
- **Context for ambiguous lines.** Pass `include_context: true`, and if the response has `needs_context: true`, send the recent conversation in a follow-up request.
- **Implicit harm.** `implicit_labels` covers content that is harmful without saying so, returned on plans that include implicit moderation, which Premium does.

A minimal request:

```bash
curl -X POST https://supervisor.gg/api/moderate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "you are an 1d10t",
    "enabled_labels": ["insult", "toxicity", "harassment"]
  }'
```

## Keep the word list, but demote it

A classifier does not mean deleting your list. Exact-match lists remain useful for things that are about identity rather than meaning: your own brand names, specific competitor names, a handful of terms your community has agreed it never wants. Run the classifier for meaning, keep a short list for the specifics.

## Do not rely on normalisation alone

You can strip zero-width characters and map homoglyphs to ASCII before matching. It helps, and it is worth doing. It also becomes its own maintenance job, because the substitution space is large and it does nothing for abuse that uses no banned word at all.

## Summary

- Word lists lose to any trick that changes the string.
- Test your filter against substitutions, homoglyphs, zero-width characters and spacing with the script above.
- Use labels and `enabled_labels` instead of a growing list, and keep a short list for the specifics.

Read the [API reference](/docs/integrations/api), try your own bypasses in the [live demo](https://supervisor.gg/demo), or [create a free account](https://supervisor.gg) and get an API key.
