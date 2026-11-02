---
title: "Supervisor vs Wick: server security and content moderation compared"
date: 2026-08-29
description: "Wick is a Discord security bot: anti-nuke, anti-raid, quarantine and verification. Supervisor now has a free security suite covering most of that, plus AI content moderation. An honest comparison, including what Wick still does that Supervisor does not."
---

# Supervisor vs Wick: server security and content moderation compared

*Updated 2 November 2026: Supervisor now includes anti-nuke, anti-raid, verification, backups and
the rest of a [security suite](/blog/supervisor-security-suite). This comparison has been
rewritten to match. When it was first published, Supervisor had none of these.*

**Bottom line:** Wick is a security bot, and it remains a very good one. Supervisor now covers
most of Wick's security features free (anti-nuke, join gate, Heat spam filtering, lockdown,
quarantine, verification and moderation commands with numbered cases), with the advanced tier
(panic mode, join raid detection, backups, heat tuning) included in Supervisor Premium. On top of
that, Supervisor reads what messages mean, which Wick's Heat system does not. For most servers
one bot now covers both halves. Wick still has things Supervisor does not: an appeals site, member
reports, a 35-event logger, a Discord AutoMod panel and a rescue key, plus a long track record.

When we first wrote this comparison the answer was "run both", because the two tools barely
overlapped. Wick was a security bot and Supervisor was a content moderation bot. That changed on
2 November 2026, when Supervisor added a security suite. The overlap is now large, so this is an
honest look at where the two still differ.

## Quick comparison

| | Wick | Supervisor |
| --- | --- | --- |
| Protects against | Structural attacks and spam | Structural attacks, spam and harmful meaning |
| Anti-nuke | **Yes, its core feature** | Yes, free |
| Panic mode | Yes | Yes, Premium |
| Join raid detection | Yes | Yes, Premium |
| Join gate filters | Yes | Yes, free |
| Verification and quarantine | Yes | Yes, free |
| Backups and restore | Yes | Yes, Premium |
| Spam filter | Heat, a decaying rate score | Heat, a decaying rate score, free |
| Ban, kick and case tracking | Yes | Yes, free |
| Reads what a message means | No | **Yes, 16 AI labels** |
| Conversation context | No | **Yes** |
| Images and video | Attachment heat only | **Yes, reads content** |
| Appeals, member reports, 35-event logger | **Yes** | No |
| Entry price | Free, or $5 a month for Premium | Security free; AI moderation and Advanced Security in Premium at £13.99 a month |

## What Wick actually is

Wick's own documentation is clear about where it puts its weight. The feature it names as "the
critical feature that differentiates Wick from all other Discord Bots" is its **Anti-Nuke
system**: a monitoring system watching channel and role creation and deletion, bans and kicks,
and webhook creation and deletion, aimed squarely at rogue admins and compromised accounts rather
than ordinary members.

Around that sit:

- **Panic Mode**, which locks the server down the moment a nuke attempt is detected, handing
  complete authority to the owner and Wick while it works out who was responsible. Wick deploys a
  separate "miniWick" to gather pre-nuke server state so the main bot is not overloaded.
- **The Restore System**, which reloads the most recent backup of your server, reverting deletions
  made during the attack. Wick's docs are candid that without Imaging enabled the restore "is a
  finicky process and lacks a lot of information and the server may not be restored properly".
- **Quarantine**, which strips power from a suspected rogue admin or member. Attempts to bypass
  quarantine, to add dangerous permissions to any role, or to change the vanity URL all result in
  quarantine themselves.
- **Verification**, **Lockdown**, **Backups**, and a moderation command set covering Ban, Kick,
  Purge, Timeout, Sanitize, Slowmode, Notes and Warn, with case tracking.

Its automod is a system Wick calls **Heat**. Rather than fixed thresholds, every action adds heat
that decays over time, and enough heat triggers a punishment. Wick describes it as "an adaptive
algorithm that adjusts to the user's current actions and scales properly with an increase in
members and their activity", with the analogy of a machine gun that overheats and then cools.
Heat is contributed by normal messages, message repetition, emojis, characters, new lines,
mentions (with `@everyone` weighted heavily), attachments, inactivity in quiet channels, a words
blacklist, a links blacklist, advertisement, NSFW websites, malicious websites including
IP-grabbers and keyloggers, and what Wick calls hidden factors.

This is genuinely impressive engineering, and the heat model is a better answer to spam than a
fixed counter. Wick's docs note it "rarely generates false positives, unlike conventional
methods", and the reasoning behind that claim, that heat decays so ordinary chatter never
accumulates enough, is sound. It is a good enough idea that Supervisor's own spam filter now
works the same way.

## Where a security model stops

The limits are not flaws, they are the boundary of what the tool is for.

**Heat is a rate and behaviour model, not a meaning model.** Wick's own documentation says the
system is "completely message based" in the sense of counting message events and their properties.
It measures how much, how fast, how repetitive, how many mentions, how many emojis. It does not
ask what a message says. So a single calmly written message, correctly spelled, sent at a normal
pace, generates almost no heat no matter what it contains. That is exactly the shape of a targeted
threat, a grooming attempt, or a well-written scam.

**The blacklists are still lists.** Words Blacklist and Links Blacklist catch what you wrote
down, spelled the way you wrote it. The usual evasions apply: `fr33 n1tr0`, `h8`, `5c4m`,
`h a t e`, `s.c.a.m`, homoglyphs, invisible characters. And you need a list per language.

**There are no harm categories.** Nothing in the heat model classifies harassment, hate, threats
or self-harm as things in their own right. The advertisement, NSFW and malicious-website factors
are the closest it comes, and those are about links rather than what a person is saying to
another person.

**Nothing weighs conversation context.** Heat accumulates per user, not per conversation, so a
message that is only harmful given what came before it reads the same as any other.

## What Supervisor does now

Supervisor has two parts.

**A security suite, free for every server, using no credits.** It never calls the AI models, so
it keeps working if a server runs out of credits or switches AI moderation off:

- **Anti-nuke** watching the audit log, with per-minute and per-hour limits on channel and role
  creation and deletion, bans, kicks and webhook creation and deletion. The punishment is yours to
  choose: log only, timeout, kick, ban or quarantine. It also holds quarantine in place, protects
  the vanity URL (it punishes the change, but cannot change the URL back itself), reverts
  dangerous permissions added to public roles or to @everyone in a channel, and filters bots added
  by anyone other than the owner and trusted users. Anti-nuke is off until you switch it on.
- **A join gate** for account age, missing profile pictures, unverified bots, invite links in
  names, a username word filter, and harmful usernames flagged by Supervisor's username model.
- **Heat**, a decaying spam score built from repeats, emojis, length, new lines, mentions,
  attachments, invites and links on the Discord-AntiScam phishing and malware list.
- **Auto lockdown** on mention raids, plus `/lock` and `/unlock`.
- **Quarantine** and **verification** by web, captcha image or button.
- **Moderation commands**: `/ban`, `/kick`, `/timeout`, `/warn`, `/purge`, `/slowmode`,
  `/sanitize`, `/note` and more, with every action recorded as a numbered case, plus warn
  thresholds that act automatically.

**Advanced Security, included in Supervisor Premium.** Panic mode (deleting what the attacker
created in the last hour, locking the server and restoring from the latest backup), strict mode,
prune detection, join raid detection, heat tuning and heat panic mode, role and full lockdown,
automatic backups with `/backup`, and captcha customisation. There is no separate security plan.

**AI content moderation**, the paid, credit-using part, with purpose-built models that read what
a message means:

- It catches leetspeak, homoglyphs, invisible characters and creative spelling, because it reads
  intent rather than exact strings.
- It has implicit moderation for harm that is implied rather than stated, and it can weigh recent
  conversation history when a message is ambiguous on its own.
- It classifies across 16 labels: harassment, hate, threats, scams, spam, promotional content,
  sexual content, self-harm, illegal activity and more.
- It moderates images and video, reading what is in the picture.
- It works in over 100 languages without a separate rule set per language.

You do not write or maintain any of it.

## What Wick does that Supervisor does not

The list is much shorter than it was, but it is real.

- **An appeals site.** Wick gives banned members a way to appeal. Supervisor does not.
- **Member reports.** Supervisor has no way for members to report messages.
- **A 35-event logger.** Supervisor logs its own security and moderation actions, but has no
  general Discord event logger and no message edit or delete logs.
- **A Discord AutoMod panel.** Supervisor does not manage AutoMod rules.
- **A rescue key**, custom permit levels, Imaging, and the ID-pattern and string-flag join raid
  algorithms.
- **Vanity URL restore.** Both punish a vanity URL change. Supervisor cannot set the old URL back.
- **A long track record.** Wick has protected servers for years. Supervisor's security suite is
  new as of November 2026.

## Wick guards the door. Supervisor now does both.

Wick's job is the perimeter and the blast radius: who gets in, who holds power, what happens when
someone turns hostile, and how you put the server back together afterwards. It is a focused,
mature product for exactly that.

Supervisor now covers most of that perimeter too, and then carries on past it. Once the members
are legitimate, nobody is raiding and no admin has gone rogue, the question becomes what people
are actually saying to each other, which is a question about meaning rather than about
permissions or rates. Wick does not try to answer that one.

## Why trust this comparison

Everything above about Wick comes from Wick's own material: the features page of
docs.wickbot.com for anti-nuke, panic mode, the restore system and the Heat model, including the
quotes, plus the command reference and the premium page. All read on 29 August 2026. Its public
rating on top.gg was 84 out of 100 from 259 ratings on the same date, on top.gg's 0 to 100 scale.

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
100 languages, conversation context, and the only one that reads images and video. Its security
suite covers most of Wick's feature list, but not appeals, member reports, the event logger, the
AutoMod panel or the rescue key, and it has no utility features such as levels, tickets or
reaction roles.

We have no customer reviews, ratings or testimonials to show you, because we have not collected
any. Judge it on your own content in the [live demo](https://supervisor.gg/demo) rather than on
our word for it.

## For developers and platforms

Wick is a Discord security bot, so it has no application outside Discord. Supervisor has a REST
API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api) has
the endpoints and the current rates.

## So which should you use?

For most servers, Supervisor now covers both halves on its own: anti-nuke, join gate, Heat,
lockdown, quarantine, verification and case-tracked moderation free, with panic mode, raid
detection and backups in Premium, and AI moderation that reads what members actually post: the
harassment spelled to dodge a blacklist, the scams, the implied threats, the harmful images and
video, and the single calm message that generates no heat at all.

Wick is still the better fit if you rely on its appeals site, member reports, 35-event logging,
AutoMod panel or rescue key, or if you want a security bot with years of history behind it.
Running Wick for those extras alongside Supervisor's AI moderation is still a perfectly good
setup.

Want to see the difference on your own content? Paste a message that gets past a keyword filter
into the [live demo](https://supervisor.gg/demo) and watch it get caught, or
[add Supervisor to your server](https://invite.supervisor.gg).
