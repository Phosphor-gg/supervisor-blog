---
title: "How to stop a Discord raid: what to do now and how to prevent the next one"
date: 2026-11-16
description: "A step by step guide to handling a Discord raid while it is happening, cleaning up afterwards, and setting up your server so the next one fails."
---

# How to stop a Discord raid: what to do now and how to prevent the next one

**Bottom line:** During a raid, stop new people getting in first (pause invites or raise your
verification level), then stop the people already inside from posting (lock channels or turn on
slowmode), then remove the raiders and clean up. Afterwards, put the defences in place before
you need them: a sensible verification level, Discord's AutoMod, a join gate, a spam filter and
an automatic lockdown, so the next raid is handled in seconds rather than by whoever happens to
be awake.

A raid is a burst of accounts joining your server at once, usually to flood channels with spam,
slurs, shock images or mass mentions. It is different from a nuke, where someone with
permissions destroys the server from the inside. If that is what you are dealing with, read
[anti-raid vs anti-nuke](/blog/anti-raid-vs-anti-nuke) instead.

## During a raid: step by step

Work in this order. Each step makes the next one easier.

### 1. Stop new accounts getting in

Every second invites stay open, more raiders arrive. You have two quick options in Discord
itself.

- **Pause invites.** Discord lets a server pause invites, which, in Discord's words, prevents
  "new users from joining" ([Discord developer docs, guild features](https://docs.discord.com/developers/resources/guild)).
  Discord's documentation says this can be set for at most 24 hours ahead.
- **Raise the verification level.** Discord's levels range from "unrestricted" up to "must have
  a verified phone number", with steps for a verified email, accounts registered "for longer than
  5 minutes", and members of the server "for longer than 10 minutes"
  ([Discord developer docs, verification level](https://docs.discord.com/developers/resources/guild)).
  Fresh throwaway accounts struggle with the higher levels.

### 2. Stop the accounts already inside from posting

- **Lock the busiest channels** by denying Send Messages to @everyone, or lock them all.
- **Turn on slowmode.** Slowmode is the number of seconds a member has to wait between
  messages, anywhere from 0 to 21,600 (six hours) ([Discord developer docs, channel object](https://docs.discord.com/developers/resources/channel)).
  Even a short delay turns a flood into a trickle.

### 3. Remove the raiders

Raids tend to share tells: accounts created minutes ago, no profile picture, matching or
patterned usernames, all joining within the same minute. Sort your member list by join date and
ban the batch. Banning rather than kicking matters, because a kicked account can come straight
back.

### 4. Clean up the mess

Delete the spam in bulk rather than message by message, check whether any webhooks or invites
were created, and look at your audit log for anything a raider should not have been able to do.
If a raider could change roles or channels, the problem is your permissions, not just the raid.

### 5. Reopen carefully

Unlock channels one at a time, lower verification again if you raised it, and resume invites.
Tell your members what happened in one short message. Then work through the prevention steps
below while it is fresh.

## How to prevent the next raid

### 1. Set a verification level you can live with

For most public servers, requiring a verified email or a minimum account age blocks the laziest
raids without bothering real members. Keep the phone verification level for when you are under
attack.

### 2. Turn on Discord's AutoMod

AutoMod is built in and free. Its rule types include a mention spam rule that checks "if content
contains more unique mentions than allowed", a generic spam rule, preset word lists, up to six
custom keyword rules, and a rule for member profiles
([Discord developer docs, AutoMod](https://docs.discord.com/developers/resources/auto-moderation)).
Actions are blocking the message, sending an alert to a channel, or a timeout. The mention spam
rule alone defeats a lot of ping raids.

### 3. Gate joins

A join gate checks each member as they arrive. Supervisor's join gate, free on every server,
can act on accounts younger than a minimum age, accounts with no profile picture, unverified
bots, invite links in usernames, a username word list with wildcards (look-alike letters are
folded before matching), and usernames its username model flags as harmful. Each filter has its
own action.

### 4. Catch floods automatically

Raids are floods, and floods are a rate problem. Supervisor's heat filter adds heat for repeated
messages, emojis, mentions, @everyone, attachments, invites and known phishing links, and cools
every second, so normal chat never builds up. Reaching the limit is an automatic timeout with
the spam deleted. **Auto lockdown** locks channels for you when mentions flood in.

With Advanced Security, included in Supervisor Premium, **join raid detection** acts on a surge
of joins as a group (ten in a minute by default, or whatever you set) and can lock new joins for
ten minutes, and **heat panic mode** drops the heat limit to a quarter for half an hour when
several members hit it close together.

### 5. Prepare your commands

Know how you will lock down before you need to. Supervisor's `/lock` locks one channel, every
channel, or new joins, and `/unlock` removes only what the lock added. `/purge` deletes in bulk
with filters for one member, bots, links, attachments, mentions, or members with no roles, and
`/ban` works by ID for accounts that have already left. Every action is a numbered case, so you
have a record afterwards.

### 6. Consider verification for suspicious accounts

Supervisor's Cloudflare verification can apply only to suspicious accounts, new or without an
avatar, so everyone else gets straight in. Unverified members can be removed after a time limit.

## Where Supervisor fits

Discord's own tools are the first line and you should use them. A bot adds what they do not
do: acting on a whole wave of joins at once, scoring floods rather than single messages, and
locking down without a moderator online. Supervisor's security features never call its AI models,
so they use no credits. The base set is free for every server, and Advanced Security is part of
Supervisor Premium at £13.99 a month. On top of that, Supervisor's AI moderation reads what
messages mean, which catches the raider who posts one calm, nasty message instead of a flood.

Other security bots do much of this too, and some have features Supervisor does not, such as an
appeals site and a full event logger. Use whatever your team will actually configure.

Want to see how Supervisor reads messages that slip past a filter? Try the
[live demo](https://supervisor.gg/demo), or [add Supervisor to your server](https://invite.supervisor.gg)
and switch on the join gate and heat before your next raid.

## Frequently asked questions

### What is the fastest way to stop a Discord raid?

Pause invites or raise your verification level so no more raiders can join, then lock or slow
your busiest channels. Banning and cleaning up can wait a minute; stopping the inflow cannot.

### Should I kick or ban raiders?

Ban them. A kicked account can rejoin through any open invite, while a ban keeps that account out
for good.

### Does Discord's AutoMod stop raids?

It helps, especially its mention spam rule, which blocks messages with too many unique mentions.
It works message by message, though, so it does not act on a wave of joins as a group.

### How do I stop raids while my moderators are asleep?

Set up automatic defences: a join gate, a spam filter that times out flooders, and an automatic
lockdown on mention floods. Supervisor does all three on the free plan, with join raid detection
in Premium.

### Does Supervisor's raid protection use credits?

No. None of the security features call the AI models, so they use no credits and keep working if
your server runs out of credits or switches AI moderation off.
