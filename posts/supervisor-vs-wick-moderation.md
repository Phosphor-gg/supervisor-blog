---
title: "Supervisor vs Wick: server security versus content moderation"
date: 2026-08-29
description: "Wick is a Discord security bot: anti-nuke, anti-raid, quarantine and verification. Supervisor moderates message content. An honest comparison of two tools that solve different halves of the same problem."
---

# Supervisor vs Wick: server security versus content moderation

Of all the comparisons we could write, this is the one where the honest answer is least of a
contest. Wick is a security bot. Supervisor is a content moderation bot. They protect against
different things, and a server with a serious problem in one area is not helped by the other.
This is an honest comparison, and the short version is that they are not really the same kind of
tool, more than in any other pairing we have looked at.

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
accumulates enough, is sound.

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

## What Supervisor does differently

Supervisor moderates with purpose-built AI models that read what a message means:

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

This list is longer than in any other comparison we have written, and it should be.

- **Anti-nuke.** Supervisor has nothing remotely like it. No monitoring of role or channel
  deletion, no rogue admin detection, no vanity URL protection.
- **Anti-raid and panic mode.** Supervisor has no raid protection at all.
- **Server backups and restore.** Supervisor cannot restore anything.
- **Quarantine, verification and lockdown.** None of these exist in Supervisor.
- **Ban and kick.** Supervisor's actions are Delete, Timeout and Warn only.
- **Case tracking and notes.** Supervisor sends alerts to a channel and does not keep a case file.
- **Malicious and phishing link detection as a maintained feature.** Supervisor's link filter
  covers Discord invites, media, Nitro gifts and your own domain allow and block lists.

If your server's problem is that someone with permissions might destroy it, or that a raid might
overwhelm it, Supervisor is not the answer and we would rather say so.

## Wick guards the door. Supervisor reads the room.

This is the honest framing. Wick's job is the perimeter and the blast radius: who gets in, who
holds power, what happens when someone turns hostile, and how you put the server back together
afterwards. It does that better than anything else in this category.

Supervisor's job starts after all of that has gone right. The members are legitimate, nobody is
raiding, no admin has gone rogue, and the server is running normally. The question then is what
people are actually saying to each other, which is a question about meaning rather than about
permissions or rates.

Almost nobody choosing between these two is really choosing. They are two halves.

## For developers and platforms

Wick is a Discord security bot, so it has no application outside Discord. Supervisor has a REST
API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API for provisioning
moderation to your own users. The [API reference](https://supervisor.gg/docs/integrations/api) has
the endpoints and the current rates.

## So which should you use?

For most servers with either problem, the answer is both, and unusually here that is not a hedge.

Use Wick if your risks are structural: raids, nukes, rogue admins, compromised accounts,
alt-account floods, or a need to verify people at the door and restore the server if something
goes wrong. That is its entire design and it is very good at it.

Reach for Supervisor when the members are legitimate and the problem is what they are posting: the
harassment spelled to dodge a blacklist, the scams, the implied threats, the harmful images and
video, the abuse in languages your lists do not cover, and the single calm message that generates
no heat at all. Supervisor is the AI moderation layer that reads meaning, and it sits alongside
your existing setup rather than replacing your security bot.

Want to see the difference on your own content? Paste a message that gets past a keyword filter
into the [live demo](https://supervisor.gg/demo) and watch it get caught, or
[add Supervisor to your server](https://invite.supervisor.gg).
