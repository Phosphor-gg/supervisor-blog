---
title: "Supervisor vs MEE6: AI moderation versus all-in-one automod"
date: 2026-08-29
description: "MEE6 is the most widely used all-in-one Discord bot, with eight automod checks and a full enforcement ladder. An honest comparison with Supervisor, an AI moderation bot, including what MEE6 does better."
---

# Supervisor vs MEE6: AI moderation versus all-in-one automod

MEE6 is probably the most recognised bot on Discord, and for a lot of servers it was the first
bot they ever added. It does levels, social alerts, giveaways, economy, custom bot
personalisation and moderation, all from one dashboard. If you are comparing it specifically on
moderation, it is worth being precise about what its automod does, because that is where
Supervisor takes a different approach. This is an honest comparison, and the short version is
that they are not really the same kind of tool.

## What MEE6's moderation actually is

MEE6's Moderator plugin has two halves: an automod ruleset that watches messages, and an
enforcement system that acts on accumulated warnings.

The automod ruleset is eight checks:

- **Bad Words**, scanning messages against a list of pre-defined words or phrases.
- **Repeated Text**, for the same message sent too frequently.
- **Server Invites**, detecting and removing Discord invites.
- **External Links**, removing messages containing links out.
- **Excessive Caps**, with a default threshold of 70% capitals.
- **Excessive Emojis, Spoilers, and Mentions**, as one combined check.
- **Zalgo**, for stacked combining characters.
- **Anti-Spam**, a separate feature watching message frequency.

Each check can be set to Disabled, Delete Message, Warn Member, or Delete Message and Warn
Member, and each can be scoped with "deny for all roles except" and "allow for all channels
except" style rules, plus server-wide immunity roles.

The enforcement half is where MEE6 is genuinely strong. Automated actions escalate on warning
counts inside a time window, applying the first matching rule, ordered by severity. MEE6's own
examples are ten warnings in fourteen days for a permanent ban, five in seven days for a
three-day ban, and two in twenty four hours for a one-day mute. Moderators get `/ban`,
`/tempban`, `/kick`, `/clear`, and an infractions system, all backed by an audit log covering
around two dozen event types.

This is genuinely good tooling, and the escalation ladder in particular is more than most
moderation products offer, ours included.

## Where an eight-check ruleset hits its ceiling

Every one of those checks is either a string match or a counter, and that sets the ceiling.

**A word list only catches what you wrote down, spelled the way you wrote it.** Anyone trying to
get past Bad Words does not type the listed word. They type around it:

- Leetspeak and substitutions: `fr33 n1tr0`, `h8`, `5c4m`.
- Unicode look-alikes: Cyrillic or Greek letters that read identically to a person but are
  entirely different characters to a filter.
- Zero-width and invisible characters inserted mid-word.
- Spaced out or punctuated: `h a t e`, `s.c.a.m`.

Every one of those defeats a word list the moment it ships, and you need a fresh list for every
language your community speaks.

**Counters measure volume, never meaning.** Repeated Text, Excessive Caps, Excessive Emojis and
Anti-Spam all ask "how many" and never "what". Which means the single most damaging message in
your server is invisible to them. A targeted threat, a grooming attempt, or a convincing scam is
one calmly written, correctly spelled message with no banned word, no caps, no emoji and no
repetition. Every counter reads zero.

**There are no harm categories.** Nothing in the eight checks identifies harassment, hate,
threats, self-harm or scams as things in their own right. Those become word lists you write and
maintain.

**Nothing weighs conversation context.** Each check judges one message alone, so "do it then" or
"nobody would miss you" read identically whether they follow a joke or an argument.

## What Supervisor does differently

Supervisor moderates with purpose-built AI models instead of lists and counters. It reads what a
message means, so the evasion tricks have nothing to trick and the single harmful message is not
invisible:

- It catches leetspeak, homoglyphs, invisible characters and creative spelling, because it reads
  intent rather than exact strings.
- It has implicit moderation for harm that is implied rather than stated, and it can weigh recent
  conversation history when a message is ambiguous on its own.
- It classifies across 16 labels, covering what no check expresses: harassment, hate, threats,
  scams, spam, promotional content, sexual content, self-harm, illegal activity and more.
- It moderates images and video, reading what is in the picture rather than counting attachments.
- It works in over 100 languages without a separate word list per language.

You do not write or maintain any of it. There is no list to keep current and no arms race to
lose.

## What MEE6 does that Supervisor does not

This matters more than winning the comparison, because you will find out either way.

- **MEE6 can ban and kick.** Supervisor's actions are Delete, Timeout and Warn. There is no ban,
  no kick, and no equivalent of MEE6's warning-count escalation ladder.
- **MEE6 has a real audit log.** Supervisor sends alerts to a channel. It is not a logging suite.
- **MEE6 does everything else too.** Levels, economy, giveaways, birthdays, social alerts, bot
  personalisation. Supervisor has three slash commands and no utility features at all.
- **MEE6 sells a lifetime plan.** Supervisor is subscription only.
- **MEE6 refunds for 7 days.** Supervisor offers a seven day trial instead, which is a different
  arrangement.

## Lists are for words. Supervisor is for meaning.

This is the honest way to frame it. MEE6's checks are the right instrument for the countable and
matchable: invite spam, caps, emoji walls, repeated text, links you do not allow. Those are
volume and string problems, and eight checks plus an escalation ladder handles them well.

They do nothing about the quietly written message that contains no listed word and trips no
counter, because that message is not a string problem. Catching a flood and catching a threat
are different problems, and you can run both tools at once.

## For developers and platforms

MEE6 is a Discord bot, so it does not help you moderate your own product. Supervisor has a REST
API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api)
has the endpoints and the current rates.

## So which should you use?

They solve different jobs, and for a lot of servers the answer is both.

Use MEE6 for what it is great at: the enormous feature set beyond moderation, the enforcement
ladder, the audit trail, and rule-based automod for exact, countable things. If that covers what
your server actually struggles with, MEE6 on its own is fine, and its moderation works without
paying.

Reach for Supervisor when rule-based automod is not catching the content that hurts your
community: the harassment spelled to dodge the word list, the scams, the implied threats, the
harmful images and video, the abuse in languages your rules do not cover, and the single message
that trips no counter at all. Supervisor is the AI moderation layer that reads meaning, and it
sits alongside your existing setup rather than replacing your utility bot.

If cost is part of the decision, we have broken down [what MEE6 costs](/blog/mee6-pricing),
including the per server licensing and which headline rate actually renews.

Want to see the difference on your own content? Paste a message that gets past a keyword filter
into the [live demo](https://supervisor.gg/demo) and watch it get caught, or
[add Supervisor to your server](https://invite.supervisor.gg).
