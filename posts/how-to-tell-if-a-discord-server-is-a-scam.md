---
title: "How to tell if a Discord server is a scam"
date: 2026-11-16
description: "The warning signs of a scam Discord server, from hijacked invite links and fake staff to QR codes and requests for your token, and how to protect yourself and your own community."
---

# How to tell if a Discord server is a scam

**Bottom line:** A scam server wants one of three things from you: your account, your money,
or something you run on your computer. The giveaways are consistent: an invite that does not
come from the project's own channels, pressure to act fast, staff who message you first, links
that are almost right, QR codes, and any request for your password, token or a download. If a
server asks for any of those, leave it and report it.

Discord's own [Community Guidelines](https://discord.com/guidelines) forbid using Discord "to
promote, coordinate, or execute financial scams", which it defines as "any intentionally
deceptive act taken with the intent to receive an illegal, unethical, or otherwise dishonest
gain". The signs below are how those servers tend to show themselves.

## Where did the invite come from?

Most scam servers are reached through a link someone handed you, so start there.

**Check the official source.** A real project, game or creator lists its server on its own
website or social accounts. If the invite came from a stranger's DM or a reply under a popular
post, find the official link yourself and compare.

**Be wary of old vanity links.** Discord's
[scam guidance](https://discord.com/safety/protecting-users-from-scams-on-discord) explains
that if a Partnered, Verified or boosted server loses its custom invite, "nefarious communities
may swoop in and claim your old one". An old link in a years-old tweet may not lead where it
used to. Discord tells server owners to keep their official invites updated and visible on
every platform for this reason.

**Look at the link itself.** Discord's example of a fake is "dliscordnltro.com", a misspelling
designed to pass a quick glance. It also warns that "link shortening services can easily mask
unsafe websites or programs".

## Warning signs once you are inside

**Staff message you first.** Real moderators rarely open a DM to offer you something. Discord
lists "they never posted in any of your mutual servers... but they want to speak to YOU" as a
classic sign, and a compromised moderator account can be used to "impersonate you to trick
unsuspecting members", in Discord's own words. A familiar name is not proof.

**Everything is urgent.** Limited spots, a mint closing in ten minutes, a prize you must claim
now. Discord flags people who "seem in a rush and are warning you that you gotta get in on what
they're offering fast or you'll lose out".

**You are told to verify through a link, QR code or program.** Discord's advice is "Don't scan
any QR codes from people you don't know or those you can't verify as legitimate" and "Don't
download programs or copy/paste code you don't recognize." A verification step that asks you
to log in to Discord on another site, scan a code, or paste something into your browser console
is the scam.

**Someone asks for your password or token.** Discord is blunt: "Don't give your password to
anyone!" and "Never share or screenshare your authorization token." Nothing legitimate needs
either.

**A bot looks slightly off.** Discord warns to "be vigilant for bots that are impersonating
larger well-known bots". A "verification bot" with a familiar name that DMs you a login link
deserves suspicion.

**"Special access" offers.** Discord's line is worth remembering: "If it sounds too good to be
true, it probably is."

**The server is locked down except for one channel with a link.** Scam servers often hide
everything except an announcement or verification channel, so you cannot see what other
members are saying.

## If you have already clicked something

1. **Change your password** and turn on two factor authentication. Discord "strongly
   recommend[s] enabling 2FA" and notes that with it on, a hacker would also need a 2FA code
   to change your password.
2. **Report what happened.** Discord's
   [reporting guide](https://discord.com/safety/how-to-report-content-to-discord) explains
   how to report a message: right click it on desktop, or hold it on mobile, and select
   "Report Message". Discord's scam page says reporting can also help you regain ownership of
   a taken account.
3. **Report any bot involved.** Open the app's profile, use the three dot menu and select
   "Report App", as described in Discord's
   [guide to reporting applications](https://discord.com/safety/reporting-applications-to-discord).
4. **Warn your friends.** A taken account is used to message its contacts next.

## If you run a server

Your community can be targeted from inside your own server, through a compromised moderator
account or a raid of fresh accounts posting phishing links. Discord's checklist for owners is
short: "Audit your server Permissions, especially for higher-level tools like webhooks", make
sure only trusted moderators hold powerful permissions, and keep your official invites up to
date. It also notes that "any large and reputable moderation bot will never need admin
permissions to work properly", so give bots only the permissions their job needs.

## Where Supervisor fits

Supervisor cannot tell you whether a server you are about to join is a scam. It works inside
servers that have added it, and its job there is to stop your own members from being scammed
and your server from being turned into a scam. The relevant parts:

- The **heat filter** adds heat for Discord invites and for links on a maintained public list
  of phishing and malware domains, along with repeated messages and mention floods, and times
  out anyone who reaches the limit. It is free and uses no credits.
- **AI moderation** reads the meaning of a message across 16 labels and over 100 languages, so
  a polite "DM me to claim your reward" is judged on what it says rather than on keywords.
- **Anti-nuke** watches the audit log for mass channel, role, webhook, ban and kick actions and
  quarantines the account responsible by default. Its permission monitoring reverts dangerous
  permissions added to @everyone, and its bot addition filter removes bots added by anyone
  other than the owner or a trusted user. That is the path attackers use when a moderator
  account is compromised.
- The **join gate** and, with Advanced Security, **join raid detection** deal with waves of
  fresh accounts arriving to spam links.

There are gaps worth knowing about: Supervisor has no way for members to report messages and no
message edit and delete logging yet. The full list is in our
[security suite announcement](/blog/supervisor-security-suite).

## Frequently asked questions

### How can I check if a Discord invite is real?

Find the invite on the project's own website or official social accounts and compare it with
the one you were given. Discord notes that old custom invites can be claimed by other servers,
so an old link is not proof.

### Is a server asking me to verify a scam?

Not always, since many genuine servers use verification. It is a scam if verifying means
logging in to Discord on another site, scanning a QR code, downloading a program or pasting
code into your browser.

### What do scammers want with my Discord token?

Your token lets someone act as your account without your password. Discord says never to share
or screenshare it, and no genuine server or bot will ask for it.

### A moderator DMed me with an offer. Is that safe?

Be cautious. Discord warns that compromised accounts are used to impersonate their owners, so
check the offer in the server's public announcements before you act on it.

### How do I report a scam server?

Report the messages involved using "Report Message", report any bot through its profile with
"Report App", and leave the server. Discord's Safety Center has guides for both.

### Can Supervisor protect my server from scam links?

Supervisor's heat filter acts on Discord invites and on links to known phishing and malware
domains, and its AI moderation reads scam messages that contain no link at all. It works inside
servers that have added it, not on servers you are thinking of joining.

## Protect your community

Try Supervisor's moderation on the [live demo](https://supervisor.gg/demo), or
[add it to your server](https://invite.supervisor.gg). The security features are free and use
no credits.
