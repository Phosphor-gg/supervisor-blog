---
title: "MEE6 vs Dyno vs Supervisor: engagement, control, or AI moderation"
date: 2026-08-29
description: "Most people land here choosing between MEE6 and Dyno. Here is the honest answer on that, backed by both bots' own documentation, plus a third option that does a different job."
---

# MEE6 vs Dyno vs Supervisor: engagement, control, or AI moderation

**Bottom line:** pick Dyno if moderation decides it, because it documents 19 automod filters
against MEE6's 8 and gives all of them away free. Pick MEE6 if you want levels, social alerts
and an audit trail alongside. Add Supervisor when messages get past both, because neither reads
what a message means.

Most people arrive at this comparison choosing between MEE6 and Dyno, the two best known general
purpose Discord bots. That is a real decision with a real answer, so this post resolves it first,
then covers a third option that does a different job to either.

Everything below about MEE6 and Dyno comes from their own documentation and pricing pages, checked
on 29 August 2026. We make Supervisor, so treat the third section accordingly.

## The short answer

- **Pick MEE6** if you want engagement features alongside moderation: levels, economy, giveaways,
  birthdays and social alerts across six platforms, with a solid warning-escalation ladder and a
  thorough audit log.
- **Pick Dyno** if moderation configurability is the priority. Nineteen automod filters against
  MEE6's eight, all free, with a full ban and mute ladder included.
- **Add Supervisor** if the messages hurting your community are not the countable kind, and both
  bots' filters are reading zero on them.

## At a glance

| | MEE6 | Dyno | Supervisor |
| --- | --- | --- | --- |
| What it is | All-in-one | General purpose | AI moderation layer |
| Automod mechanism | 8 rule checks | 19 rule filters | 16 AI labels |
| Reads meaning | No | No | Yes |
| Conversation context | No | No | Yes |
| Images and video | Not documented | Image spam counts only | Yes, reads content |
| Can ban or kick | Yes | Yes | No |
| Free tier includes automod | Yes | Yes | No, 7 day trial |
| Billing unit | Per server | Per server | Per account |
| Entry price | £11.99 / month | $5.99 / month | £13.99 / month |
| Languages | Word lists you write | Word lists you write | 100+ |

## MEE6 vs Dyno: the differences that actually matter

### Automod depth

This is the clearest split. **Dyno documents nineteen automod filters**: All Caps at a default 70%
threshold, Bad Words, Chat Clearing Newlines, Duplicate Text, Character Count, Emoji Spam, Fast
Message Spam, Image Spam, Invite Links, Known Phishing Links, Links, Links Cooldown, Mass
Mentions, Mentions Cooldown, Spoilers, Masked Links, Stickers, Sticker Cooldown and Zalgo Text.
You can create several rules for the same filter with different actions.

**MEE6 documents eight checks**: Bad Words, Repeated Text, Server Invites, External Links,
Excessive Caps at the same 70% default, a combined Excessive Emojis, Spoilers and Mentions check,
Zalgo, and a separate Anti-Spam feature.

If you want to enforce a specific countable rule, Dyno probably has a filter for it and MEE6
probably does not. Dyno also gives you Known Phishing Links as a maintained detection, which MEE6
does not document.

### Enforcement style

Both can ban and kick, and they escalate differently.

**MEE6 escalates on accumulated warnings** inside a time window, applying the first matching rule
ordered by severity. Its own examples are ten warnings in fourteen days for a permanent ban, five
in seven days for a three-day ban, and two in twenty four hours for a one-day mute. That is a
graduated policy expressed in one place.

**Dyno escalates per rule.** Each filter gets Warn, Delete, Auto Mute, Auto Ban, Instant Mute or
Instant Ban, with Auto actions firing after a violation count you set. Dyno's own documentation
notes an important detail: the Automod Warn action "is not a `?warn` and will not dm the user, be
logged in the Modlog channel, appear on `?warnings` or `?modlogs`, or go toward any Autopunish
settings", and automod violations expire after 5 minutes.

So MEE6 gives you one coherent ladder across the server. Dyno gives you finer control per rule but
keeps automod warnings separate from its manual warning system. If you want an infraction history
that everything feeds into, MEE6's model is simpler to reason about.

### What you pay, and for what

Both are per server, which matters most if you run several.

**MEE6** is £11.99 a month, £49.99 a year, or £89.99 once for lifetime, with the standard rates
shown here in pounds because that is what it displayed to us. Its FAQ confirms per server
licensing: "A subscription is valid for a single Discord server."

**Dyno** is $5.99 a month or $49.99 a year for Standard, described as "for one server of your
choice", rising to $7.99 and $12.99 monthly for higher tiers.

Different currencies, so compare in whichever you actually pay in. What is comparable is what the
money buys. **Dyno's paid tier barely touches detection**: Advanced Automod adds per-rule log
channels and custom responses, while all nineteen filters and the full ban ladder are free.
**MEE6's paid tier is broader** but also mostly not about automod, since its checks are free too.
MEE6 alone offers a lifetime purchase.

### Verdict on MEE6 versus Dyno

**If moderation is the deciding factor, pick Dyno.** More filters, finer control, everything that
matters free, and phishing link detection MEE6 does not document.

**If you want the server to do more than be moderated, pick MEE6.** Levels, economy, giveaways,
social alerts across Twitch, X, YouTube, RSS, Reddit and Instagram, and an audit log covering
around two dozen event types. Dyno has modules too, but MEE6's engagement side is the reason most
servers install it.

Detailed breakdowns either way: [what MEE6 costs](/blog/mee6-pricing) and
[what Dyno costs](/blog/dyno-bot-pricing).

## Where both hit the same ceiling

Whichever you pick, you inherit the same blind spot, because both are rule engines.

**Word lists only catch what you wrote down.** MEE6's Bad Words and Dyno's Banned Words fail on
identical input: `fr33 n1tr0`, `h8`, `5c4m`, `h a t e`, `s.c.a.m`, Cyrillic look-alikes, zero-width
characters. Dyno's own documentation illustrates the trap neatly, since its wildcard mode matches
inside other words, so banning "hi" also matches "high", while exact mode misses every evasion.

**Counters measure volume, never meaning.** Fast Message Spam, Mass Mentions, Excessive Caps,
Repeated Text and Anti-Spam all ask how many and how fast. The single most damaging message in a
server is usually one calm, correctly spelled sentence that trips nothing.

**Neither classifies harm by category.** There is no harassment filter, no threat filter, no scam
filter, no self-harm filter in either product. Those become word lists you maintain, in every
language your community speaks.

**Neither weighs conversation context.** "Do it then" and "nobody would miss you" read identically
whether they follow a joke or an argument.

Switching between MEE6 and Dyno does nothing about any of that.

## What Supervisor adds, and what it does not

Supervisor is an AI moderation layer rather than a general purpose bot. Instead of matching strings
and counting events, it reads what a message means: 16 labels including harassment, hate, threats,
scams, spam, sexual content, self-harm and illegal activity, conversation context and implicit
moderation for messages that are ambiguous alone, image and video moderation that reads content
rather than counting attachments, and over 100 languages without a word list per language. It is
billed per account at £13.99 a month, or about £4.99 on the three year cycle, so one subscription
covers every server you run.

What it does not do, and this list matters:

- **No bans or kicks.** Delete, Timeout and Warn are the whole set, so neither MEE6's warning
  ladder nor Dyno's Auto Ban has an equivalent.
- **No counters.** Caps percentages, emoji counts, newlines, character limits and message rates
  are not measured at all.
- **No utility features.** Three slash commands, no levels, no social alerts, no giveaways, no
  audit log suite, no autoroles.
- **No free tier for new accounts**, just a seven day trial and £0.25 of moderation on signup.
- **It deletes after a message posts**, where Discord's own AutoMod blocks before.

The detail on each pairing is in [Supervisor vs MEE6](/blog/supervisor-vs-mee6-moderation) and
[Supervisor vs Dyno](/blog/supervisor-vs-dyno-moderation).

## So which should you use?

**Running one bot:** Dyno if moderation control matters most, MEE6 if engagement features do.
Both are free at the level most servers need.

**Running one bot and unhappy with what gets through:** the answer is not the other bot. Add a
layer that reads meaning, and keep the rule engine for the countable work.

**Running a network of servers:** note that both MEE6 and Dyno multiply per server, while
Supervisor is one subscription for the account. That changes the arithmetic quickly.

**The setup we would actually recommend** for a large, busy server: Discord AutoMod on for the
free block-before-posting, MEE6 or Dyno for the countable rules and the enforcement ladder, and an
AI layer for the messages that read as harmless to a counter. Three tools, three jobs, and none of
them replacing another.

## Why trust this comparison

Everything above about MEE6 and Dyno comes from their own material: MEE6's Moderator plugin
documentation and premium pages, and Dyno's automod and moderation documentation plus its pricing
page. All read on 29 August 2026. On top.gg's 0 to 100 scale Dyno was 87 from 373 ratings that
day; MEE6 publishes no top.gg rating.

We make Supervisor, so this is not a neutral comparison and we have not written it as one. What we
have done instead is put the other side's advantages in their own section above, in plain terms,
and say where we could not read something rather than guessing at it.

On our own side, the figures come from our source and our evaluation set rather than from
marketing copy. Supervisor's models are retrained on real moderation feedback, the thumbs up and
thumbs down votes people leave on live flags in their own servers, which is the closest thing to
customer research this category has. The last full retrain moved average F1 across the 16 labels
from 0.794 to 0.941 on our internal evaluation set, with errors on harmless messages down 44
percent, and version 2.2 improved macro-F1 again across all three model tiers. The method and the
per-label numbers are in the [2.1 release post](/blog/supervisor-2-1).

**Where Supervisor leads, and where it does not.** On moderation coverage specifically it is the
most complete tool in this series: 16 labels where nothing else classifies more than four, over
100 languages, conversation context, and the only one that reads images and video. It is also the
narrowest, with no bans, no raid protection and no utility features, which is why every post here
recommends running it alongside another bot rather than instead of one.

We have no customer reviews, ratings or testimonials to show you, because we have not collected
any. Judge it on your own content in the [live demo](https://supervisor.gg/demo) rather than on
our word for it.

## For developers and platforms

MEE6 and Dyno are Discord bots, so neither helps you moderate your own product. Supervisor has a
REST API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api) has
the endpoints and the current rates.

Whichever you pick, test it on your own content rather than on a feature table. Paste a message
that gets past a keyword filter into the [live demo](https://supervisor.gg/demo) and watch it get
caught, or [add Supervisor to your server](https://invite.supervisor.gg).
