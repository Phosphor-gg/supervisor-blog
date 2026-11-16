---
title: "How to tell if a Discord account is a bot"
date: 2026-11-16
description: "The difference between a legitimate Discord app and a user account run by a script, the signs that give automated accounts away, and what to do about them in your server."
---

# How to tell if a Discord account is a bot

**Bottom line:** There are two kinds of bot on Discord. Apps are legitimate, have an app
profile, and can be reported as an app. The ones to worry about are ordinary user accounts
driven by a script, which Discord's own Community Guidelines forbid. You usually cannot prove
an account is automated from one message, but a handful of signs together (no history in
shared servers, an unnatural way of talking, urgency, a link) are a strong signal, and you
can stop most of them at the door.

## Two kinds of bot

Discord describes applications as things you "may know as bots that automate tasks", and
they are a normal part of the platform. Moderation bots, music bots and levelling bots are
all apps. Server admins choose to add them, and Discord's Terms of Service say it is "your
choice whether to use these third-party services". Every app has a profile, and Discord's
[guide to reporting applications](https://discord.com/safety/reporting-applications-to-discord)
explains that you can open that profile, click the three dot menu and select "Report App" if
one breaks the rules.

The other kind is a normal user account controlled by software. Discord's
[Community Guidelines](https://discord.com/guidelines) are direct about this: "Do not use
self-bots or user-bots. Each account must be associated with a human, not a bot." The same
guidelines forbid sending spam and selling "spambots, server 'raid' tools, account-creation
tools, token generators" and similar tools.

So when people ask whether an account is a bot, they almost always mean the second kind: a
user account that looks like a person but is not one. That is what the rest of this post is
about.

## Signs an account is automated

None of these proves anything alone. Real people are new, shy, or have no avatar. Look for
several at once.

**It messages you out of nowhere.** Discord's own
[scam guidance](https://discord.com/safety/protecting-users-from-scams-on-discord) describes
the pattern: "They never posted in any of your mutual servers, or don't even share mutual
servers with you, but they want to speak to YOU." Scripted accounts tend to join a large server,
scrape the member list and work through it by direct message.

**The writing does not sound human.** The same page lists "their speaking patterns aren't the
most human" as a warning sign. Watch for replies that ignore what you said, the same opening
line sent to several people, or a conversation that moves straight to a link.

**It is in a hurry.** Discord flags accounts that "seem in a rush and are warning you that you
gotta get in on what they're offering fast or you'll lose out". Urgency is there to stop you
thinking, which is the point.

**It makes claims about you.** Another of Discord's examples is an account that claims "you did
things you know you have never done", such as reporting you or owing money, followed by a link
to "sort it out".

**It posts the same thing in many channels quickly.** A burst of identical messages across a
server, often with an invite or a link, is what a spam script does and what a person rarely
does.

**Its profile is empty and its name is odd.** No avatar, a brand new account, and a username
that is a random string or contains an invite link are common for throwaway accounts. They are
also common for real newcomers, so treat this as a reason to look closer, not a verdict.

**It pretends to be something it is not.** Discord warns server owners to "be vigilant for
bots that are impersonating larger well-known bots". A user account named after a popular bot,
or after one of your staff, is a red flag.

## What to do if you think an account is a bot

1. **Do not click its links or run anything it sends.** Discord's advice is plain: "Don't
   click links from unknown senders or that look suspicious" and "Don't download programs or
   copy/paste code you don't recognize."
2. **Never share your password or token.** Discord's words are "Never share or screenshare
   your authorization token. Seriously. Don't do it."
3. **Report it.** Discord's
   [reporting guide](https://discord.com/safety/how-to-report-content-to-discord) says to
   right click a message on desktop, or hold it on mobile, and select "Report Message". If it
   happened in a server, you can also tell that server's moderators.
4. **Block it.** The same page reminds you that you "always have the ability to ignore or
   block any users".
5. **Tighten who can message you.** Discord suggests you "consider restricting who can DM
   with you" in its scam guidance.

## Keeping automated accounts out of your server

If you run a server, you see these accounts in bulk rather than one at a time. The useful
question is not "is this one a bot" but "how do I make my server a poor target".

**Audit what new members can do.** Discord tells server owners to "audit your server
Permissions, especially for higher-level tools like webhooks" and to make sure only
moderators you trust have powerful permissions. A fresh account that cannot post links or
mention everyone does far less damage.

**Gate new joins.** Many spam accounts are young, have no avatar, or carry an invite in their
name. A join check that holds or removes those accounts stops a lot of them before they post.

**Watch for surges.** One automated account is a nuisance. Fifty joining in a minute is a
raid, and needs handling as a group rather than one ban at a time.

**Rate limit the flood.** Automated accounts post fast and repetitively. Something that
notices repeated messages, mention floods and invite spam catches them by behaviour, without
needing to know who they are.

## Where Supervisor fits

Supervisor is an AI moderation and security bot for Discord, and several of its free
features are aimed squarely at automated accounts. To be clear about what it does not do:
it cannot look inside another account and tell you whether a script is driving it. Nothing
outside Discord can. What it can do is act on the signs above.

- The **join gate** checks every member as they arrive, with its own action per filter:
  accounts younger than a minimum age, accounts with no profile picture, unverified bots,
  invite links in usernames, a username word list (look-alike letters are folded before
  matching), and usernames Supervisor's username model flags as harmful.
- **Join raid detection** (Advanced Security, part of Premium) acts on every account in a
  surge of joins, and can lock new joins for ten minutes.
- The **heat filter** adds heat for repeated messages, mentions, @everyone, invites and links
  on a maintained list of phishing and malware domains, and times out anyone who reaches the
  limit. It measures how someone posts, not what they say.
- **Verification** can send only suspicious accounts (new, or without an avatar) through a
  Cloudflare check on supervisor.gg, and remove members who do not verify in time.
- **AI moderation** reads what people actually write, across 16 labels and over 100
  languages, so a calm message pushing a scam is still caught even when it trips no rate
  limit.

The join gate, heat filter, verification and moderation commands are free and use no
credits. Full details are in our [security suite announcement](/blog/supervisor-security-suite).

## Frequently asked questions

### Are all bots on Discord against the rules?

No. Apps that server admins choose to add, such as moderation or music bots, are a normal part
of Discord. What Discord's Community Guidelines forbid is self-bots and user-bots, meaning
ordinary user accounts controlled by software.

### Can I tell for certain that an account is a bot?

Usually not from the outside. You can see strong signals, such as no shared server history,
unnatural replies, urgency and a link, but only Discord can see how an account is actually
being operated.

### What should I do if a bot sends me a link?

Do not click it, and do not download or run anything it sends. Report the message to Discord,
block the account, and tell the moderators of any server you share with it.

### How do I report a bot that is an app?

Open the app's profile, click the three dot menu and select "Report App". Discord's guide to
reporting applications walks through the options for desktop, web and mobile.

### Does an account with no profile picture mean it is a bot?

Not by itself. Plenty of real people never set an avatar. It is worth noticing when it comes
together with a brand new account, an odd username and an unprompted message with a link.

### Can Supervisor stop bot accounts joining my server?

Supervisor's join gate can act on new accounts, accounts with no avatar, invite links in
usernames and harmful usernames, and its heat filter catches spam by behaviour. It cannot tell
you how another account is being run, but it makes your server a much poorer target.

## Try it

See how Supervisor reads messages on the [live demo](https://supervisor.gg/demo), or
[add it to your server](https://invite.supervisor.gg) and switch on the join gate and heat
filter in a couple of minutes.
