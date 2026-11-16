---
title: "Is MEE6 safe?"
date: 2026-11-16
description: "An honest look at whether MEE6 is safe to add to your Discord server: the permissions it asks for, the 2022 NFT server incident, what we could and could not verify about its data handling, and how to limit risk with any bot."
---

# Is MEE6 safe?

**Bottom line:** We found no source showing that MEE6's own systems have been breached, and it
is a long-established bot. In the best known incident, in 2022, MEE6 said publicly that there
was "no technical breach in our systems". The real risk with MEE6, as with any bot, is the
permissions you hand it: its help pages suggest the Administrator permission for convenience,
and you do not have to accept that. Give it only what the features you use need, and read its
privacy policy before you add it.

We make a competing moderation bot, so treat this as an interested party's view. Every claim
about MEE6 below comes from MEE6's own help pages or from reporting we could read, with links,
and where we could not verify something we say so.

## What MEE6 is

MEE6 is an all-in-one Discord bot covering moderation, levels, custom commands and more,
configured from a web dashboard. Its [wiki FAQ](https://wiki.mee6.xyz/faq) describes it as
offering "a wide range of features, including moderation, leveling, custom commands, and more",
and says you add it by clicking "Add to Discord" on the MEE6 website. It also notes that "you
need to have administrator permissions on your Discord server to invite bots". For a broader
look at what it does well, see our [MEE6 review](/blog/mee6-review).

## The permissions question

This is where safety is actually decided, for MEE6 and every other bot.

A bot can only do what its role allows. MEE6's help article on
[the Manage Roles permission](https://help.mee6.xyz/en/articles/611744-mee6-is-missing-manage-roles-permission)
tells you to find the MEE6 role in your server settings and make sure it has Manage Roles for
role features. It then adds: "To make managing your MEE6 bot much easier, you can enable a
single permission called 'Administrator'."

That is a convenience suggestion, not a requirement, and it is worth thinking about before you
follow it: Administrator is the widest permission there is. Discord's own
[scam guidance](https://discord.com/safety/protecting-users-from-scams-on-discord) is clear on
the general principle: "In almost every case, any large and reputable moderation bot will never
need admin permissions to work properly. Only give a bot the permissions required for the tasks
you need and no more."

Giving a bot Administrator does not make the bot itself malicious. It raises the stakes if
anything that can control that bot is ever misused, which is exactly what the 2022 incident
below was about.

## The 2022 NFT server incident

In May 2022 several NFT and crypto Discord servers, including Axie Infinity's, posted fake
"mint" announcements carrying phishing links, and MEE6 was named in the reporting.
[Vice reported](https://www.vice.com/en/article/hackers-compromise-a-string-of-nft-discord-channels)
that MEE6 denied its systems were breached and attributed the unwanted posts to one of its
employee's accounts being compromised, quoting MEE6: "There is no technical breach in our
systems."
[Cointelegraph's report](https://cointelegraph.com/news/axie-infinity-s-discord-bot-compromised-hackers-issue-fake-minting-message)
says MEE6's support channel denied it had been hacked and that its engineers saw no unusual
activity.

Accounts of exactly what happened differ between sources, and we could not find a detailed
post-mortem from MEE6, so we will not go further than that. Two things are fair to take from
it. First, it is more than four years old and we found no comparable incident since. Second,
the general lesson applies to every bot: a bot with powerful permissions is a powerful tool for
whoever manages to control it, whether through the bot itself or through an admin account on
your server. Keeping permissions narrow limits the damage either way.

## What data MEE6 handles

We tried to read MEE6's privacy policy for this post and could not load it: the URLs we tried
returned not found pages, and searches did not surface the current policy. So we are not going
to describe what MEE6 collects or how long it keeps it. Check the policy linked from MEE6's own
website before you add it, and ask MEE6's support if anything is unclear.

As a general point, any moderation bot needs to read messages to moderate them, and any
levelling bot needs to record activity to count it. The question for any bot is what it keeps,
for how long, and who it shares it with, and that answer belongs in its privacy policy.

## How to limit risk with MEE6 or any bot

1. **Add it from the official site.** Discord warns to "be vigilant for bots that are
   impersonating larger well-known bots". Use the "Add to Discord" button on MEE6's website
   rather than an invite someone sent you.
2. **Untick Administrator.** On the Discord authorisation screen, grant only what the plugins
   you use need. If a feature reports a missing permission, MEE6's help pages tell you which one.
3. **Place its role carefully.** Keep MEE6's role below your staff roles, high enough for the
   role features you use and no higher.
4. **Protect the admin accounts.** Most server takeovers start with a compromised person, not a
   compromised bot. Discord "strongly recommend[s] enabling 2FA".
5. **Audit webhooks and permissions.** Discord tells owners to "audit your server Permissions,
   especially for higher-level tools like webhooks".
6. **Remove plugins and bots you no longer use.** Fewer moving parts means fewer ways in.

## Where Supervisor fits

Supervisor is not a replacement for MEE6's levels, social alerts or custom commands, and many
servers run both. Where it helps with safety is in protecting your server whichever bots you
use. Its free **anti-nuke** watches the audit log for mass channel, role, webhook, ban and kick
actions and quarantines the account responsible by default. Its permission monitoring reverts
dangerous permissions added to @everyone or to a role most of the server holds, and its bot
addition filter removes bots added by anyone other than the owner or a trusted user. With
Advanced Security, part of Premium, panic mode cleans up and restores from backup. Its AI
moderation reads what members write, across 16 labels and over 100 languages. Details are in
our [security suite announcement](/blog/supervisor-security-suite).

Supervisor's anti-nuke cannot protect you from trusted users, so keep that list short, and the
same advice on narrow permissions applies to Supervisor as to MEE6.

## Frequently asked questions

### Has MEE6 been hacked?

In May 2022 MEE6 was named in reporting about fake announcements in NFT servers. MEE6 said
there was "no technical breach in our systems" and attributed the posts to a compromised
employee account, and we found no comparable incident since.

### Does MEE6 need Administrator?

MEE6's help pages suggest Administrator to make managing the bot easier, but they also list the
specific permissions features need, such as Manage Roles. Discord's own advice is that reputable
moderation bots almost never need admin permissions.

### Does MEE6 read my messages?

Any bot that moderates or counts messages for levels has to read them. We could not load MEE6's
privacy policy, so check it directly for what is stored and for how long.

### Is it safe to give MEE6 Manage Roles?

Manage Roles is what MEE6's help pages ask for to make role features work. Keep MEE6's role
below your staff roles, so the roles it manages are not your most powerful ones.

### What is the safest way to add MEE6?

Use the "Add to Discord" button on MEE6's own website, grant only the permissions your chosen
plugins need, and turn on two factor authentication for every admin account in your server.

## Protect your server

Supervisor works alongside MEE6. Try its moderation on the [live demo](https://supervisor.gg/demo),
or [add it to your server](https://invite.supervisor.gg) and switch on anti-nuke for free.
