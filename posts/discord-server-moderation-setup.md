---
title: "How to set up moderation on a Discord server"
date: 2026-11-16
description: "A practical setup guide for a new or growing Discord server: roles and permissions, verification, AutoMod, a moderation bot, logs and rules."
---

# How to set up moderation on a Discord server

**Bottom line:** Set up moderation in this order: roles and permissions first, then a
verification level, then Discord's AutoMod, then a moderation bot for what AutoMod does not do,
then a private log channel, then short rules your team can actually enforce. Doing permissions
first matters most, because every other tool depends on who can do what. A small server can get
through all six steps in an afternoon.

## 1. Roles and permissions

This is the foundation. Mistakes here are how servers get nuked.

- **Keep Administrator rare.** Discord's docs describe it as allowing "all permissions" and
  bypassing "channel permission overwrites" ([Discord developer docs, permissions](https://docs.discord.com/developers/topics/permissions)).
  Only the owner and perhaps one co-owner need it.
- **Build a moderator role with only what moderators use**: timing out, kicking, banning,
  managing messages. Discord's Moderate Members permission is what allows timing out users "to
  prevent them from sending or reacting to messages" (same source).
- **Mind the role order.** Discord says a bot "can only kick, ban, and edit nicknames for users
  whose highest role is lower than the bot's highest role" (same source). Your moderation bot's
  role must sit above the members it moderates.
- **Require two factor authentication for moderation.** Discord lets a server require 2FA for
  moderation actions ([Discord developer docs, MFA level](https://docs.discord.com/developers/resources/guild)),
  so a stolen password alone cannot ban your members.
- **Keep @everyone boring.** It should never hold permissions like Manage Roles, Manage Channels,
  Manage Webhooks or Mention Everyone.

## 2. Verification level

Discord's verification levels go from "unrestricted" through a verified email, an account
"registered on Discord for longer than 5 minutes", membership "for longer than 10 minutes", to "a
verified phone number" ([Discord developer docs, verification level](https://docs.discord.com/developers/resources/guild)).
For most public servers, a verified email or the five minute rule is a good default. Save the
strictest level for an active raid.

While you are in server settings, look at the explicit media filter. Discord can scan media from
members without roles, from all members, or not at all (same source). Scanning all members is the
safer choice for a public server.

## 3. AutoMod

AutoMod is free and runs inside Discord, so turn it on. According to Discord's docs it offers a
mention spam rule, a generic spam rule, preset word lists, up to six custom keyword rules (each up
to 1,000 keywords) and a member profile rule, with actions to block the message, alert a channel,
or time the member out ([Discord developer docs, AutoMod](https://docs.discord.com/developers/resources/auto-moderation)).

A sensible starting set:

1. Mention spam on, with a timeout.
2. The preset word lists that suit your community.
3. One keyword rule for things specific to your server, such as rival invite names.
4. Alerts going to a private moderators channel.

Keyword rules only match what you write down, spelled the way you wrote it. That is the limit to
keep in mind for step 4.

## 4. A moderation bot

A bot covers what Discord's built in tools do not. When choosing one, decide which of these you
actually need.

### Security

Anti-nuke, a join gate, raid handling, lockdown and quarantine. Supervisor has all of these free:
anti-nuke on the audit log with per minute and per hour limits, a join gate with account age,
avatar, username and bot filters, a heat based spam filter, auto lockdown on mention floods, and
quarantine. Advanced Security, included in Supervisor Premium, adds panic mode, join raid
detection, heat tuning and automatic backups.

### Moderation commands and cases

You want one place where every action is recorded. Supervisor has `/ban`, `/kick`, `/timeout`,
`/warn`, `/purge` with filters, `/slowmode`, `/note` and more, and every action, whether a
moderator's or an automatic one, becomes a numbered case you can search. Warn thresholds act
automatically when a member collects too many warns.

### Content moderation

This is where word lists run out. Supervisor's AI moderation reads what a message means across 16
labels, including harassment, hate, threats, scams and self-harm, in over 100 languages. It
catches creative spellings and look-alike characters, can weigh recent conversation when a
message is ambiguous, and reads images and video. This part uses credits and is included in
Supervisor Premium at £13.99 a month with £120 of moderation credits.

### Setting Supervisor up

1. [Invite Supervisor](https://invite.supervisor.gg) and open your server on the
   [dashboard](https://supervisor.gg/dashboard/integrations/discord).
2. Run `/security status` to see missing permissions and whether its role is high enough. Drag
   its role near the top.
3. Run `/security setup` to create the quarantine role.
4. Add a short list of trusted users, then switch on anti-nuke, the join gate and heat.

## 5. Logs

You need a private record of what moderators and bots did. Create a staff only channel for
AutoMod alerts and another for your bot's actions. Discord's audit log already records server
changes, so get used to checking it.

Be clear about what your bot logs. Supervisor logs its own security and moderation actions as
cases, but it does not log message edits and deletions or general server events. If you want
those, add a logging bot for them.

## 6. Rules

Short rules get read. Aim for five to ten, each one something a moderator can point to.

1. Say what is not allowed, in plain words: harassment, hate, spam, NSFW outside marked channels,
   advertising without permission.
2. Say what happens: for example, a warning, then a timeout, then a ban.
3. Say how to contact staff.
4. Pin the rules where new members land, and keep them consistent with what your bot actually
   enforces.

Then write a one page guide for your moderators: when to warn, when to time out, when to ban, and
to always leave a reason so the case makes sense later.

## Where Supervisor fits

Supervisor is meant to cover steps 4 and part of 5 in one bot: security, moderation commands with
cases, and AI moderation that reads meaning. What it does not do is just as important: there is
no appeals site, no member reports, no message edit and delete logging, no panel for Discord's
AutoMod rules, and no utility features like levels or tickets. Plenty of servers run Supervisor
alongside another bot for those.

Paste a message that gets past your keyword rules into the
[live demo](https://supervisor.gg/demo), or [add Supervisor to your server](https://invite.supervisor.gg).

## Frequently asked questions

### What permissions should Discord moderators have?

Usually timing out, kicking, banning and managing messages, and nothing that changes the server's
structure. Keep Administrator for the owner and, at most, one co-owner.

### Is Discord's AutoMod enough on its own?

For a small, quiet server it can be. It matches keywords and spam patterns, so it misses creative
spellings and anything harmful that does not contain a listed word, which is where an AI
moderation bot helps.

### Why can my bot not ban some members?

Discord only lets a bot act on members whose highest role is below the bot's highest role. Move
the bot's role higher in your role list.

### What verification level should a new server use?

A verified email or the five minute account age level suits most public servers. Raise it
temporarily if you are being raided.

### Is Supervisor free?

The security suite and moderation commands are free for every server and use no credits. AI
moderation and Advanced Security are included in Supervisor Premium at £13.99 a month.
