---
title: "Dyno vs Wick vs Supervisor: rules, security, or AI moderation"
date: 2026-08-29
description: "Dyno and Wick get compared constantly and solve different problems. Here is the honest answer from both bots' own docs, and where an AI moderation layer fits alongside them."
---

# Dyno vs Wick vs Supervisor: rules, security, or AI moderation

**Bottom line:** Dyno and Wick solve different problems, so a server with both usually runs
both. Dyno moderates members with 19 countable filters, Wick defends the server against nukes,
raids and rogue admins. Add Supervisor for the harm neither reads, because a threshold and a heat
score both measure rate rather than meaning.

Dyno and Wick get compared a lot, usually by servers that have just been raided and are working
out what to install. They are less alike than the comparison suggests: Dyno is a general purpose
bot with an excellent rule engine, and Wick is a security bot built around anti-nuke.

This post resolves that first, from both products' own documentation, then covers a third layer
that neither is designed to provide.

## The short answer

- **Pick Dyno** if you want broad, countable moderation rules and general purpose modules, and
  your threats come from ordinary members.
- **Pick Wick** if your threat is structural: nukes, rogue admins, raid floods, or you need a
  verification gate and the ability to restore a wrecked server.
- **Add Supervisor** if the harm is in what legitimate members are saying, which neither a
  threshold nor a heat score reads.

## At a glance

| | Dyno | Wick | Supervisor |
| --- | --- | --- | --- |
| What it is | General purpose | Security | AI moderation layer |
| Automod mechanism | 19 fixed filters | Heat, decaying score | 16 AI labels |
| Anti-nuke | No | **Yes, its core** | No |
| Panic mode and lockdown | No | **Yes** | No |
| Backups and restore | No | **Yes** | No |
| Verification and quarantine | No | **Yes** | No |
| Phishing link detection | **Yes, maintained** | Malicious site heat | Own block lists only |
| Reads meaning | No | No | **Yes** |
| Conversation context | No | No | **Yes** |
| Images and video | Image spam counts | Attachment heat | **Yes, reads content** |
| Can ban or kick | **Yes** | **Yes** | No |
| Free tier includes automod | **Yes** | **Yes** | No, 7 day trial |
| Entry price | $5.99 / month per server | $5 / month | £13.99 / month per account |

## Dyno vs Wick: the differences that actually matter

### They are not solving the same problem

This is the thing to settle before comparing features.

**Dyno moderates members.** Its nineteen automod filters watch what people post: All Caps, Bad
Words, Chat Clearing Newlines, Duplicate Text, Character Count, Emoji Spam, Fast Message Spam,
Image Spam, Invite Links, Known Phishing Links, Links, Links Cooldown, Mass Mentions, Mentions
Cooldown, Spoilers, Masked Links, Stickers, Sticker Cooldown and Zalgo Text.

**Wick protects the server.** Its documentation calls anti-nuke "the critical feature that
differentiates Wick from all other Discord Bots", and it monitors channel and role creation and
deletion, bans and kicks, and webhook creation and deletion. Its target is the rogue admin or
compromised account, not the member posting too many emojis.

If someone with permissions starts deleting channels, Dyno does not notice. If someone posts a
wall of zalgo text, Wick's heat system notices but does not have a dedicated filter for it.

### Two different anti-spam philosophies

Both handle spam, and the mechanisms are genuinely different.

**Dyno uses fixed thresholds.** Fast Message Spam triggers on x messages in a 5 second window in a
single channel. Mass Mentions on x mentions in one message. Image Spam on multiple images within
10 seconds. You set the numbers.

**Wick uses Heat**, an accumulating score that decays over time. Its docs describe it as "an
adaptive algorithm that adjusts to the user's current actions and scales properly with an increase
in members and their activity", with a machine gun overheating analogy. Heat comes from message
repetition, emojis, characters, new lines, mentions with `@everyone` weighted heavily,
attachments, inactivity in quiet channels, blacklisted words and links, advertisement, NSFW
websites and malicious websites. Wick claims it "rarely generates false positives, unlike
conventional methods".

The heat model is mechanically better for spam, because a burst of genuine excitement cools off
while sustained abuse accumulates, where a fixed threshold punishes both identically. Dyno's model
is more predictable and easier to explain to your moderators.

### Enforcement

Both ban and mute. **Dyno** offers Warn, Delete, Auto Mute, Auto Ban, Instant Mute and Instant Ban,
with Auto actions on a violation count, and free-tier limits of 3 autopunishments, 14 day mutes and
3 month bans. **Wick** has Ban, Kick, Timeout, Purge, Quarantine, Sanitize, Lockdown and Warn, with
Auto Timeouts that escalate and a Multiplier making each punishment harsher so raiders cannot wait
out a fixed cap.

Wick's quarantine is the more interesting mechanism, because it strips power rather than removing
the person, which is the right response to a suspected compromised admin.

### Verdict on Dyno versus Wick

**They are complementary more than competitive, and most servers with both problems run both.**

If forced to choose: **pick Dyno if your incidents are members misbehaving**, since it has far more
tools for that and a much larger module set beyond moderation. **Pick Wick if your incidents are
attacks**, because nothing Dyno offers protects against a nuke, and no amount of automod matters
once your channels are deleted.

Full breakdowns: [what Dyno costs](/blog/dyno-bot-pricing), our
[Dyno review](/blog/dyno-bot-review) and [Wick review](/blog/wick-bot-review).

## Where both hit the same ceiling

Different mechanisms, same blind spot.

**Dyno's filters are strings and counters.** Its own Banned Words modes make the trade-off
explicit: exact mode misses `fr33 n1tr0`, and wildcard mode banning "hi" also matches "high".
Counters ask how many, never what.

**Wick's heat is a rate and behaviour model.** Its docs say the system is "completely message
based" in the sense of counting message events and their properties. A single calm, correctly
spelled message sent at a normal pace generates almost no heat regardless of content.

So the message that does the most damage in a healthy server, one carefully written sentence aimed
at one person, is invisible to both. Neither classifies harassment, threats, scams or self-harm as
categories. Neither weighs conversation context. Neither reads what is inside an image.

## What Supervisor adds, and what it does not

Supervisor reads what a message means rather than matching strings or measuring rate: 16 labels
including harassment, hate, threats, scams, spam, sexual content, self-harm and illegal activity,
conversation context and implicit moderation for ambiguous messages, image and video moderation,
and over 100 languages. Billed per account at £13.99 a month, or about £4.99 on the three year
cycle, so one subscription covers every server.

What it does not do, and against these two the list is long:

- **No anti-nuke, no panic mode, no backups, no restore, no quarantine, no verification.** Wick's
  entire category is absent.
- **No counters, thresholds or heat.** Emoji spam, caps percentages, newlines, character limits
  and message rates are not measured, so Dyno's whole filter list has no equivalent.
- **No bans or kicks.** Delete, Timeout and Warn only, where both others can ban.
- **No maintained phishing link detection.** Its link filter covers Discord invites, media, Nitro
  gifts and your own domain lists, where Dyno ships Known Phishing Links and Wick scores malicious
  sites.
- **No modules.** Three slash commands.
- **No free tier for new accounts**, where both others are free at the level most servers use.

The pairings in depth: [Supervisor vs Dyno](/blog/supervisor-vs-dyno-moderation) and
[Supervisor vs Wick](/blog/supervisor-vs-wick-moderation).

## So which should you use?

**Just been raided:** Wick, and turn on Discord AutoMod, which is free and blocks messages before
they post.

**Members misbehaving, no structural threat:** Dyno, free, and spend the afternoon configuring it.

**Both problems:** both bots. They overlap very little and neither replaces the other.

**Moderators spending their time on harassment reports rather than spam:** that is the case where
neither tool is reading the problem, and a layer that reads meaning is what closes it. Keep the
rule engine for countable work and the security bot for the perimeter.

**Running several servers:** Dyno is per server and Wick's Premium is per server too, with VIP
advertising 12 premium servers. Supervisor is one subscription for the account.

There is a related piece on [Wick alternatives](/blog/wick-bot-alternatives) that covers what does
and does not replace the security layer, and one on
[Dyno alternatives](/blog/dyno-bot-alternatives).

## Why trust this comparison

Everything above comes from the vendors' own material: Dyno's automod and moderation
documentation with its pricing page, and Wick's features page and command reference on
docs.wickbot.com. All read on 29 August 2026. On top.gg's 0 to 100 scale Dyno was 87 from 373
ratings that day and Wick 84 from 259.

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

Dyno and Wick are Discord bots, so neither helps you moderate your own product. Supervisor has a
REST API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api) has
the endpoints and rates.

Whichever layers you run, test what gets through them on your own content. Paste a message that
gets past a keyword filter into the [live demo](https://supervisor.gg/demo) and watch it get
caught, or [add Supervisor to your server](https://invite.supervisor.gg).
