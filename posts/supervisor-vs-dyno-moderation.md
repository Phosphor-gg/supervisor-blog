---
title: "Supervisor vs Dyno: AI moderation versus threshold-based automod"
date: 2026-07-26
description: "Dyno's automod is one of the most configurable rule engines on Discord: banned words, link and invite filters, spam thresholds, mass mentions, emoji and image spam, zalgo, and selfbot detection. Here is an honest comparison with Supervisor, an AI moderation bot, so you can pick the right one, or run both."
---

# Supervisor vs Dyno: AI moderation versus threshold-based automod

Dyno has been a fixture of Discord moderation for years, and its automod module is one of the most configurable rule engines you can put in a server. If you are here specifically about moderation, it is worth being precise about what Dyno's automod does and does not do, because that is exactly where Supervisor takes a different approach. This is an honest comparison, and the short version is that they are not really the same kind of tool.

## What Dyno's automod actually is

Dyno's automod is a rule and threshold engine. You tell it what to match and how many is too many, and it enforces that:

- **Banned Words**, including a default list you can disable and your own words and phrases on top.
- **Discord Invites** and **All Links**, with a link whitelist and blacklist so you can allow specific domains.
- **Masked Links**, which catches a link hidden behind display text.
- **Fast Message Spam**, triggered when someone sends several messages inside a few seconds.
- **Mass Mentions**, triggered when one message contains more than your configured number of mentions, plus a mentions cooldown for repeated mentions over a short window.
- **Image Spam** and **Emoji Spam**, both counter-based, with a max emoji count you set.
- **All Caps** and **Duplicate Text**.
- **Zalgo Text**, for the stacked combining characters that break a channel visually.
- **Spoilers** and **Selfbot Detection**, the latter flagging user messages that contain rich embeds.

On top of the filters, you choose what happens: leave a filter disabled, warn, automute, or combine them. There is an automute duration, a violation count before the mute lands, and a log channel that records who tripped what and why.

This is genuinely good tooling. For exact, countable things, a threshold engine is the right instrument. If you want nobody posting eleven mentions in one message, "more than ten mentions" is a perfect rule, and Dyno will enforce it consistently and instantly, forever, for free.

## Where rules and thresholds hit their ceiling

The catch is in the two halves of how it works.

**A word list only catches what you wrote down, spelled the way you wrote it.** People who want past a filter do not type the banned word. They type around it:

- Leetspeak and substitutions: `fr33 n1tr0`, `h8`, `5c4m`.
- Unicode look-alikes: Cyrillic or Greek letters that read identically to a person but are entirely different characters to a filter.
- Zero-width and invisible characters inserted mid-word.
- Spaced out or punctuated: `h a t e`, `s.c.a.m`.

Every one of those defeats a word list the moment it ships, and you are into an arms race, adding entry after entry while the same content keeps arriving in new spellings. You also need a fresh list for every language your community speaks.

**A threshold only measures volume, never meaning.** This is the more important half, and it is easy to miss. Counters ask "how many" and never "what". Which means:

- One message can be devastating and trip nothing. A targeted threat, a piece of harassment, a grooming attempt, or a convincing scam is a single, calmly written, correctly spelled message. It contains no banned word, one link or none, no mentions, no caps, no emoji. Every counter reads zero.
- Volume is not harm. An excited member posting five messages in five seconds about a game is not doing anything wrong, but the spam filter cannot tell them apart from a raider, because both look identical to a counter.

That second point is where the real cost shows up. Tuned tight, a threshold engine punishes enthusiasm. Tuned loose, it misses the raid. There is no setting that reads intent, because thresholds are not measuring intent in the first place.

## What Supervisor does differently

Supervisor moderates with purpose-built AI models instead of rules and counters. It reads what a message means, so the evasion tricks have nothing to trick and the single harmful message is not invisible:

- It catches leetspeak, homoglyphs, invisible characters, and creative spelling, because it reads intent rather than exact strings.
- It has implicit moderation for harm that is implied rather than stated, and it can weigh recent conversation history when a message is ambiguous on its own.
- It classifies across 16 labels, covering things no counter can express: harassment, hate, threats, scams, spam, sexual content, self-harm, and more.
- It moderates images, reading what is in the picture rather than counting how many arrived.
- It works in over 100 languages without a separate rule set per language.

You do not write or maintain any of it. There is no word list to keep current, no thresholds to re-tune after every false positive, and no arms race to lose.

## Counters are for volume. Supervisor is for meaning.

This is the honest way to frame it. Dyno's thresholds are the right tool for the countable problems: mention spam, emoji walls, raid-speed message floods, image dumps. Those are volume problems, and counters solve volume problems well.

They do nothing about the quiet, well-spelled message that does the actual damage to a community, because that message never crosses a threshold. Catching a flood and catching a threat are different problems, and you can run both tools at once.

## So which should you use?

They solve different jobs, and for a lot of servers the answer is both.

Use Dyno for what it is great at: the enormous feature set beyond moderation, and rule-based automod for exact, countable things. Invites, link policy, mention caps, emoji limits, raid-speed floods. If that covers what your server actually struggles with, Dyno on its own is fine and free to start.

Reach for Supervisor when rule-based automod is not catching the content that hurts your community: the harassment spelled to dodge the word list, the scams, the implied threats, the harmful images, the abuse in languages your rules do not cover, and the single message that trips no counter at all. Supervisor is the AI moderation layer that reads meaning, and it sits alongside your existing setup rather than replacing your utility bot.

Want to see the difference on your own content? Paste a message that gets past a keyword filter into the [live demo](https://supervisor.gg/demo) and watch it get caught, or [add Supervisor to your server](https://invite.supervisor.gg).
