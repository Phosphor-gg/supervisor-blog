---
title: "Wick bot alternatives: the honest options for server security"
date: 2026-08-29
description: "Wick is a security bot rather than a moderation bot, which makes its alternatives a shorter list than most. Here is what actually replaces it, including Supervisor's new security suite, and what only sits beside it."
---

# Wick bot alternatives: the honest options for server security

*Updated 2 November 2026: Supervisor now has anti-nuke and a full
[security suite](/blog/supervisor-security-suite), so it has moved from "sits beside Wick" to
"covers most of Wick". The rest of this list is unchanged.*

**Bottom line:** **Supervisor** is now the closest alternative to Wick: anti-nuke, join gate,
Heat, lockdown, quarantine, verification and case-tracked moderation free, with panic mode, raid
detection and backups in Premium, plus AI moderation of what members post. It does not have
Wick's appeals site, member reports, event logger, AutoMod panel or rescue key. **Sapphire's Join
Guard** is a good free option for the entry gate alone.

Wick is not a general purpose bot with a security module. It is a security bot: anti-nuke, panic
mode, backups and restore, quarantine, verification, and a spam system built on decaying heat
rather than fixed thresholds.

That makes this list different from every other alternatives post. Most Discord bots have several
close substitutes. Wick has very few, and being honest about that is more useful than padding the
list.

## Why people look for Wick alternatives

**Setup is demanding, and Wick says so.** Its own FAQ opens with "Wick is too hard to setup. Why
is that so?" and answers that the bot "can take several minutes of your time to have it completely
setup and functional as it's a sensible, customizable and an advanced bot". That is a fair warning
rather than a complaint, and it does send some people looking.

**It is priced per server.** Wick's Premium plan is $5 a month and VIP is $20 a month, with VIP
advertising 12 premium servers. Anyone running a network does the multiplication.

**It does one job.** If you want reaction roles, levels, social notifications or logging, Wick is
not that bot and you will be running something alongside it anyway.

**Its automod reads behaviour, not content.** The Heat system measures message rate, repetition,
mentions, emojis, attachments, new lines and blacklisted words and links. Excellent against
floods. Silent on a single calmly written harmful message.

## The alternatives at a glance

| Bot | What it is | Covers anti-nuke? | Free tier | Best for |
| --- | --- | --- | --- | --- |
| Wick | Security | Yes, its core feature | Yes | Raids, nukes, rogue admins |
| Sapphire | Free all-in-one | No, but has Join Guard | Yes, everything | Join filtering plus breadth |
| Dyno | General purpose | No | Yes, includes automod | Countable rules, ban ladder |
| Carl-bot | Reaction roles and moderation | No | Yes, includes automod | Flexible punishments |
| MEE6 | All-in-one | No | Yes, includes automod | Engagement plus enforcement |
| Discord AutoMod | Built into Discord | No, but has raid detection | Free, native | Blocking words before they post |
| Supervisor | Security suite plus AI moderation | Yes, free; panic mode in Premium | Security suite free; AI moderation paid | Security and what members are actually saying |

The important column is the third one. Anti-nuke is the feature Wick's own documentation calls
"the critical feature that differentiates Wick from all other Discord Bots". Apart from
Supervisor, nothing else in this table does it.

## Partial alternatives to Wick

### Sapphire

**The closest thing to a like-for-like on the entry side, and it is free.** Its **Join Guard**
uses seven filters combined with AND logic, covering account age, account creation date, default
avatars, generated names, name content, guild tags and unverified bots. That is a real gate
against alt-account floods and it is the nearest free equivalent to Wick's verification layer.

Sapphire also gives you moderation cases with warn, mute, kick and ban, logging with over 80 log
types, and genuine AI moderation for insults, threats and identity attacks, subject to its
documented limit of scanning ten messages per server per minute without the paid Limit Increase
plan.

What it does not give you is anti-nuke, panic mode, or server restore.

**Best for:** servers whose real problem was people getting in, rather than admins going rogue.

### Discord AutoMod

Free, native, and it has one relevant piece: mention raid detection, plus a spam content filter
trained on reported messages. It also blocks messages before they post, which no bot can do. It
does not watch role or channel deletion and has no restore.

**Best for:** the free baseline every server should have on regardless.

### Dyno, Carl-bot and MEE6

All three give you enforcement that Wick also has, in the form of bans, kicks and mutes, plus
automod rules and far more general purpose features. None of them monitor for nukes, none can
restore a deleted server, and none have a quarantine system.

Dyno's nineteen filters include Known Phishing Links; Carl-bot's punishments are the most flexible
in the category and its `defer` action routes ambiguous cases to a moderator vote; MEE6 escalates
on warning counts inside a time window.

**Best for:** the general purpose bot you were probably going to run next to Wick anyway.

## What only Wick and Supervisor offer

Wick's documentation describes several things that, other than Supervisor's new security suite,
nothing else in this comparison offers:

- **Anti-nuke monitoring** of channel and role creation and deletion, bans and kicks, and webhook
  creation and deletion, aimed at rogue admins rather than ordinary members.
- **Panic mode**, which locks the server down on detecting a nuke and deploys an isolated
  "miniWick" to gather pre-attack state.
- **A restore system** that reloads a backup and reverts deletions made during an attack. Wick is
  candid that without Imaging enabled this "is a finicky process and lacks a lot of information
  and the server may not be restored properly".
- **Quarantine as an escalating trap**, where bypass attempts, adding dangerous permissions to any
  role, and vanity URL changes all trigger quarantine themselves.

Supervisor now has anti-nuke with per-minute and per-hour limits on the same actions, panic mode
(Premium), backups with load and restore (Premium), and quarantine with a quarantine hold, vanity
URL protection and dangerous permission monitoring. Two differences to know: Supervisor's vanity
URL protection punishes the change but cannot set the old URL back, and it has no Imaging. Wick
also has a long track record that Supervisor's suite, released in November 2026, does not yet
have.

## Supervisor

**Supervisor** is what we make, so weigh this accordingly.

**Security, free for every server and using no credits:** anti-nuke with configurable per-minute
and per-hour limits and punishments, quarantine hold, vanity URL protection, public role and
channel permission monitoring, a bot addition filter, a join gate, Heat spam filtering with a
public phishing and malware domain list, auto lockdown, `/lock`, quarantine, verification by web,
captcha or button, and moderation commands (`/ban`, `/kick`, `/timeout`, `/warn`, `/purge`,
`/note` and more) with numbered cases and warn thresholds.

**Advanced Security, included in Supervisor Premium:** panic mode, strict mode, prune detection,
join raid detection, heat tuning and heat panic mode, role and full lockdown, automatic backups
and captcha customisation. There is no separate security plan.

**AI moderation, the paid part:** Wick's Heat system, and Supervisor's own, measure how much and
how fast, so a single well-written threat or scam generates almost no heat. Supervisor's AI reads
what a message means: 16 labels including harassment, threats, scams and self-harm, conversation
context for ambiguous messages, image and video moderation, and over 100 languages. £13.99 a
month, or about £4.99 on the three year cycle, billed per account so one subscription covers
every server you run.

What it does not have: an appeals site, member reports, a 35-event logger with message edit and
delete logs, a Discord AutoMod panel, a rescue key, custom permit levels, or Wick's ID-pattern and
string-flag join raid algorithms.

**Best for:** servers that want security and content moderation from one bot. If you rely on
Wick's appeals, reports or logging, running Wick alongside Supervisor's AI moderation also works.

## Do you actually need to replace Wick?

If you use it for anti-nuke, Supervisor now covers that free, with panic mode and restore in
Premium. If you use its appeals, reports, event logging or rescue key, nothing here replaces
those.

If you adopted it for spam and raids and have since found the setup burden heavy, Sapphire's Join
Guard plus Discord AutoMod plus a general purpose bot covers a reasonable amount of that ground for
free, though without the nuke protection or the restore.

Switching costs you your verification configuration, your quarantine setup, your backup history and
your heat tuning. That last one matters more than it sounds, because heat thresholds get calibrated
to a specific community over time.

## For developers and platforms

None of these bots help you moderate your own product, and security bots least of all since server
structure is a Discord concept. If you are building rather than buying, Supervisor has a REST API
with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints and rates.

Whatever you run at the door, test what gets past it on your own content. Paste a message that
gets past a keyword filter into the [live demo](https://supervisor.gg/demo) and see whether it
gets caught, or [add Supervisor to your server](https://invite.supervisor.gg).
