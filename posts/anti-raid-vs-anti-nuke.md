---
title: "Anti-raid vs anti-nuke: what is the difference?"
date: 2026-11-16
description: "A raid comes from outside your Discord server, a nuke comes from inside it. A plain explanation of both, and which tools cover each."
---

# Anti-raid vs anti-nuke: what is the difference?

**Bottom line:** A raid is an attack from outside: lots of new accounts join at once and flood
your channels. A nuke is an attack from inside: an account that already has permissions, often a
compromised moderator or a rogue admin, deletes channels and roles or bans members. Anti-raid
tools watch who joins and how fast people post. Anti-nuke tools watch the audit log for
destructive actions by people with power. You need both, because they defend against different
people.

## Raids, in plain terms

A raid is a crowd problem. Someone organises dozens or hundreds of accounts, many of them created
that day, to join your server together and post spam, slurs, shock images or mass mentions. None
of the raiders has any special permission. They do damage purely through volume and timing.

What a raid looks like:

- A spike of joins inside a minute or two.
- Brand new accounts, often without profile pictures, often with similar names.
- Channels flooded with the same message, pings or images.

## Nukes, in plain terms

A nuke is a trust problem. The attacker is already inside and already has permissions, so they
do not need a crowd. One account with the right role can delete every channel, every role, ban
the member list, or create webhooks to spam from. Common causes are a moderator whose account was
phished or had its token stolen, a staff member who leaves on bad terms, or a bot that was given
too much power.

What a nuke looks like:

- Channels or roles disappearing quickly.
- Mass bans or kicks from a single account.
- Dangerous permissions suddenly added to @everyone.
- New bots or webhooks nobody approved.

## Why one does not cover the other

Anti-raid defences assume the threat is a stranger. A raid filter checks account age, join
rates, and message floods. A compromised admin passes every one of those checks: their account is
old, they joined long ago, and deleting a channel is not a message.

Anti-nuke defences assume the threat is someone trusted. They count destructive actions per
account and step in when the count is too high. A raider with no permissions never triggers
them, because a raider cannot delete anything.

## What covers raids

### 1. Discord's own settings

Discord's verification levels can require a verified email, an account older than five minutes,
membership of the server for over ten minutes, or a verified phone number
([Discord developer docs, verification level](https://docs.discord.com/developers/resources/guild)).
Servers can also pause invites, preventing "new users from joining", for up to 24 hours at a time
(same source). AutoMod adds a mention spam rule and a generic spam rule
([Discord developer docs, AutoMod](https://docs.discord.com/developers/resources/auto-moderation)).

### 2. A join gate

Checks each arriving member. Supervisor's join gate, free, can act on young accounts, missing
profile pictures, unverified bots, invite links in names, a username word list, and usernames
its username model flags as harmful.

### 3. A rate based spam filter

Supervisor's heat filter scores how someone posts (repeats, emojis, mentions, attachments,
invites, known phishing links) and times out anyone who hits the limit. **Auto lockdown** locks
channels when mentions flood in.

### 4. Join raid detection

With Advanced Security (included in Supervisor Premium), Supervisor acts on a surge of joins as a
group, ten in a minute by default, and can lock new joins for ten minutes.

## What covers nukes

### 1. Permissions hygiene

Discord's own docs say Administrator "allows all permissions and bypasses channel permission
overwrites" ([Discord developer docs, permissions](https://docs.discord.com/developers/topics/permissions)).
Give it to as few accounts as possible. Discord also lets a server require two factor
authentication for moderation actions
([Discord developer docs, MFA level](https://docs.discord.com/developers/resources/guild)),
which makes a stolen password alone less useful.

### 2. An anti-nuke bot

Discord does not rate limit your own staff, so this is where a bot comes in. Supervisor's
anti-nuke, free, watches the audit log for channel and role creation and deletion, bans, kicks,
and webhook creation and deletion. Each has a per minute and per hour limit, and going over
either quarantines the account by default (or times out, kicks or bans, if you prefer). It also
reverts dangerous permissions added to @everyone or to widely held roles, holds the quarantine in
place, punishes vanity URL changes, and removes bots added by anyone other than the owner or a
trusted user.

### 3. Panic mode and backups

With Advanced Security, **panic mode** fires when anti-nuke trips a limit: it deletes the
channels, roles and webhooks the attacker created in the last hour, locks the server, turns away
new joins, and restores from the latest backup. Backups run every three hours and keep the
latest ten.

## Where Supervisor fits

Supervisor covers both halves. The base anti-raid and anti-nuke features are free for every
server and use no credits; the advanced tier is part of Supervisor Premium at £13.99 a month.
Anti-nuke is off until you switch it on, because it punishes staff, and you should keep the
trusted user list short.

It is worth being honest about the gaps. Supervisor has no appeals site, no member reports, no
message edit and delete logs, and cannot restore a vanity URL itself. Dedicated security bots
such as Wick have those, and plenty of servers run one alongside Supervisor's AI moderation.

There is also a third kind of threat neither defence catches: one member, posting normally, who
says something harmful. That is a question about meaning, not rates or permissions, and it is
what Supervisor's AI moderation is for.

Try a message in the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg) and switch on both halves.

## Frequently asked questions

### What is the difference between a raid and a nuke?

A raid is many outside accounts joining at once to flood your server. A nuke is someone inside
with permissions destroying the server, usually by deleting channels and roles or mass banning.

### Do I need anti-nuke if I trust my moderators?

Yes. Most nukes come from trusted accounts that were compromised, not from moderators turning
hostile, and anti-nuke is what limits the damage a stolen account can do.

### Can Discord's AutoMod stop a nuke?

No. AutoMod checks message content and member profiles, while a nuke is made of actions like
deleting channels and banning members, which it does not watch.

### Is Supervisor's anti-nuke free?

Yes. The anti-nuke limits, quarantine hold, permission and vanity protection and the bot addition
filter are free. Panic mode, strict mode, prune detection and backups are in Advanced Security,
included in Premium.

### Why is anti-nuke off by default?

Because it acts against your own staff. Switching it on deliberately, with a short trusted user
list, means nobody is surprised when it fires.
