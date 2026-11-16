---
title: "Is Dyno safe?"
date: 2026-11-16
description: "An honest look at whether Dyno is safe to add to your Discord server: the permissions its own docs ask for, what its privacy policy covers, and how to run it with less risk."
---

# Is Dyno safe?

**Bottom line:** We found no reported security incident involving Dyno, and it is a long-standing,
widely used bot. The thing to think about is permissions. Dyno's FAQ recommends giving it
Administrator, but it also publishes the exact list of permissions to use instead, and its
module docs list what each module needs. Use that list, keep its role in the right place, and
Dyno is as safe as a bot with moderation powers can be.

We make a competing moderation bot, so treat this as an interested party's view. Every claim
about Dyno below comes from Dyno's own documentation or legal pages, with links. Where we could
not verify something, we leave it out.

## What Dyno is

Dyno is a general purpose Discord bot with automod, moderation commands, logging, autoroles,
custom commands and more, configured from a web dashboard. Its
[FAQ](https://docs.dyno.gg/en/faq) notes that as of October 13, 2026, its prefix commands have
been removed and prefixes only work on custom commands now. For a fuller look at its features,
see our [Dyno review](/blog/dyno-bot-review).

## What permissions Dyno asks for

Dyno's [FAQ](https://docs.dyno.gg/en/faq) answers this directly: "It is recommended that Dyno
has the Administrator permission." It explains why: without Administrator, "you will also have
to ensure that Dyno has the correct permissions for every channel it has access in to ensure
commands work correctly."

It then gives the alternative. If you remove Administrator, Dyno says to make sure it always
has: Send Messages, Send Messages in Threads, Create Public Threads, Create Private Threads,
Manage Messages, Manage Threads, Read Message History, Manage Webhooks, Embed Links, Manage
Nicknames, Kick Members, Ban Members, Timeout Members, Manage Roles, Manage Channels and Manage
Permissions. It adds that "to see the permissions that a specific module requires, head to the
documentation of said module".

The module docs are more specific still. The
[Automod page](https://docs.dyno.gg/en/modules/automod) asks for Manage Webhooks, Manage Roles,
Ban Members and Timeout Members at the server level, and View Channel, Send Messages, Send
Messages in Threads, Manage Messages and Read Message History in every channel. It also says
Dyno's role must be "above the roles of the members you want it to moderate and the Muted role".

That is a long list, and it is long because Dyno does a lot: it bans, mutes, assigns roles,
manages channels and webhooks. None of it is unusual for a full moderation bot.
The choice that matters is whether you grant that list or Administrator.

Discord's own
[scam guidance](https://discord.com/safety/protecting-users-from-scams-on-discord) leans one
way: "In almost every case, any large and reputable moderation bot will never need admin
permissions to work properly. Only give a bot the permissions required for the tasks you need
and no more." Dyno's recommendation of Administrator is about avoiding broken commands from
missing channel permissions, which is a real trade-off. If you are willing to check channel
overrides, the explicit list is the tighter option.

## What Dyno's privacy policy covers

Dyno's website links to a privacy policy hosted by iubenda, titled
[Privacy Policy of Dyno & Probot](https://www.iubenda.com/privacy-policy/21925808). It names the
owner and data controller as Dyno Labs, Inc. in Los Angeles, with team@dyno.gg as the contact,
and was last updated on October 20, 2026.

The summary lists the services it uses: Google AdSense for advertising, Google Analytics and
Quantcast Measure for analytics, Sentry for infrastructure monitoring, and Google Tag Manager.
On retention, the full policy says personal data is kept "for as long as required by the purpose
they have been collected for" and that "once the retention period expires, Personal Data shall be
deleted". It also describes how to exercise rights such as access, erasure and opting out of
sale or sharing for targeted advertising.

What we could not find in the policy is a specific description of the Discord data the bot
itself handles, such as message content or logs, or how long those are kept. That does not mean
anything is wrong; it means we cannot tell you. If that matters to your community, ask Dyno at
the contact address in the policy.

## Has Dyno had a security incident?

We searched for reported breaches or vulnerabilities involving Dyno and found none from a
reputable source. Absence of reports is not a guarantee, so the steps below still apply.

## How to limit risk with Dyno or any bot

1. **Add it from dyno.gg.** Discord warns to "be vigilant for bots that are impersonating larger
   well-known bots".
2. **Use the explicit permission list** from Dyno's FAQ instead of Administrator, and add
   module-specific permissions only for modules you enable.
3. **Keep its role where its docs say,** above the members and Muted role it manages, and below
   the staff roles it has no reason to touch.
4. **Enable only the modules you use.** Every module is another set of permissions and settings.
5. **Protect your admins.** Most takeovers start with a compromised human account. Discord
   "strongly recommend[s] enabling 2FA".
6. **Audit webhooks.** Dyno's Automod asks for Manage Webhooks, and Discord tells owners to "audit your
   server Permissions, especially for higher-level tools like webhooks".

## Where Supervisor fits

Dyno's automod is one of the most configurable rule engines on Discord, and we do not suggest
replacing it. Many servers run Dyno and Supervisor together. Supervisor adds two things a rule
engine does not do. Its AI moderation reads what a message means, across 16 labels and over 100
languages, so evasive spelling and a calm threat are still caught. And its free **anti-nuke**
protects the server's structure whichever bots you run: it watches the audit log for mass
channel, role, webhook, ban and kick actions and quarantines the account responsible by default,
reverts dangerous permissions added to @everyone, and removes bots added by anyone other than the
owner or a trusted user. With Advanced Security, part of Premium, panic mode can restore from a
backup. Details are in our [security suite announcement](/blog/supervisor-security-suite).

Supervisor needs permissions to do that too, and the same advice applies: its `/security status`
command lists exactly which permissions it is missing, so you can grant those rather than
Administrator.

## Frequently asked questions

### Is Dyno a virus or malware?

We found no reputable report of Dyno behaving maliciously or being breached. It is an established
moderation bot, and the main thing to manage is how much permission you give it.

### Does Dyno need Administrator?

Dyno's FAQ recommends Administrator so commands do not break on channel permissions, but it also
publishes the list of permissions to use if you remove it. Discord's own advice is that reputable
moderation bots almost never need admin permissions.

### What data does Dyno collect?

Dyno's privacy policy lists Google AdSense, Google Analytics, Quantcast Measure, Sentry and Google
Tag Manager, and describes retention and your rights. We could not find a specific description of
bot data such as message logs, so contact Dyno at team@dyno.gg if you need that detail.

### Why does Dyno need Manage Webhooks?

Dyno's Automod documentation lists Manage Webhooks among its required server permissions, so
the module needs it to work as documented. Check your server's webhooks from time to time, whichever bots you
use.

### Can I use Dyno and Supervisor together?

Yes. Dyno handles countable rules such as caps, spam and link filters, and Supervisor adds AI
moderation that reads meaning and anti-nuke protection for the server itself.

## Protect your server

Try Supervisor's moderation on the [live demo](https://supervisor.gg/demo), or
[add it to your server](https://invite.supervisor.gg) next to Dyno and switch on anti-nuke for
free.
