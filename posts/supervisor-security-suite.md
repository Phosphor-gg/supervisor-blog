---
title: "Supervisor now protects your server, not just your chat"
date: 2026-11-02
description: "Anti-nuke, join gate, raid detection, heat spam filtering, lockdown, quarantine, captcha verification, backups and a full set of moderation commands. Free for every server, with an advanced tier included in Premium."
---

# Supervisor now protects your server, not just your chat

**Bottom line:** Supervisor now has a full security suite alongside its AI moderation:
anti-nuke, a join gate, raid detection, a heat based spam filter, lockdown, quarantine,
three verification methods, backups, and ban, kick, timeout, purge and the rest of the
moderation commands, with numbered cases. The base version of all of it is free for every
server and uses no credits. The advanced tier is included in Supervisor Premium, at no extra
cost.

Until now we told you honestly that Supervisor read what members say but did nothing about
the structure of your server. If a moderator account was compromised and started deleting
channels, Supervisor could not help. You needed a separate security bot for that, and most
servers that took security seriously ran one.

That gap is closed. Everything below is configured per server on the
[dashboard](https://supervisor.gg/dashboard/integrations/discord), like every other
Supervisor setting.

## What it costs

None of the security features call our AI models, so none of them use credits. They keep
working if your server runs out of credits or if you switch AI moderation off.

| | Free | Advanced Security (Premium) |
| --- | --- | --- |
| Anti-nuke limits, quarantine hold, vanity and permission protection, bot addition filter | Yes | Yes |
| Panic mode with automatic restore | | Yes |
| Strict role mode and prune detection | | Yes |
| Join gate | Yes | Yes |
| Join raid detection | | Yes |
| Heat spam filter | Fixed tuning | Fully tunable, timeout multiplier, heat panic mode |
| Auto lockdown on mention floods | Yes | Yes |
| Lock channels, the server or new joins | Yes | Yes |
| Lock role permissions, full lockdown | | Yes |
| Quarantine | Yes | Yes |
| Web, captcha and button verification | Yes | Yes, plus captcha styling and expiry |
| Backups, automatic and manual | | Yes |
| Moderation commands, cases, notes, warn thresholds | Yes | Yes |

Advanced Security is part of Supervisor Premium, which is £13.99 a month with £120 of
moderation credits. There is no separate security plan to buy. You can set the Premium
options on a free server now; they switch on when the server's billing admin is on Premium,
and if Premium lapses your settings are kept for when it comes back.

## Anti-nuke

Anti-nuke watches the audit log for the actions that destroy servers: creating and deleting
channels, creating and deleting roles, bans, kicks, and creating and deleting webhooks. Each
one has a per minute and a per hour limit, and going over either is treated as an attack.
The account responsible is quarantined by default, or timed out, kicked or banned if you
prefer.

It also stops the quieter moves an attacker makes:

- **Quarantine hold.** Removing the quarantine role by hand, or giving it dangerous
  permissions, is reverted and punished. Only the owner, trusted users and administrators can
  release someone with `/unquarantine`.
- **Permission monitoring.** Dangerous permissions added to @everyone, to a role most of the
  server holds, or to @everyone in a single channel are reverted and punished.
- **Vanity URL protection.** Changing the vanity URL is punished. Discord does not let a bot
  set it back, so you will need to restore it yourself.
- **Bot addition filter.** Bots added by anyone other than the owner or a trusted user are
  removed, and the person who added them is punished.

With Advanced Security, **panic mode** takes over the moment anti-nuke fires on a limit. It
deletes the channels, roles and webhooks the attacker created in the last hour, locks every
channel except the categories you exclude (tickets, for example), turns away new joins, and
restores the server from its latest backup: deleted channels and roles come back with their
permissions. It unlocks on its own after 30 minutes, or whenever you choose. **Strict mode**
extends permission monitoring to every role, and **prune detection** counts member prunes
against the limits.

Anti-nuke is off until you switch it on. It punishes staff, so it should never surprise
anyone. Add the people you trust completely as trusted users and keep that list short: a
trusted account is exempt from everything, which is exactly why it should be rare.

## Keeping raids out

The **join gate** checks every member as they arrive. Each filter has its own action:
accounts younger than a minimum age, accounts with no profile picture, unverified bots,
invite links in usernames, a username word list with wildcards (look-alike letters such as
Cyrillic е are folded before matching), and usernames Supervisor's username model flags as
harmful.

**Join raid detection** (Advanced Security) looks for surges rather than individuals. When
ten accounts join within a minute, or whatever you set, every account in the surge is acted
on, joins that keep coming are handled as they arrive, and new joins can be locked for ten
minutes.

## Heat

The heat filter is for spam and floods. Every message adds heat for what it contains:
repeating the last message, emojis, length, new lines, mentions, @everyone, attachments and
stickers, Discord invites, and links on a maintained public list of phishing and malware
domains. Heat cools every second, so normal conversation never builds up, and reaching the
limit is an automatic timeout with the spam deleted.

With Advanced Security you can tune every weight, the limit and the cooling rate, and turn on
a **multiplier** so each repeat offence in a day gets a longer timeout. **Heat panic mode**
notices when several members hit the limit close together, which is what a raid looks like,
and drops the limit to a quarter for half an hour.

Heat measures how someone posts, not what they say. That is still the job of Supervisor's AI
moderation, which reads meaning across 16 labels and over 100 languages. The two work side
by side: heat catches the flood, the model catches the one calm message that is a threat.

## Lockdown and quarantine

`/lock` locks one channel, every channel, or new joins (kick or ban), and **auto lockdown**
does it for you when mentions flood in. Blind mode hides the channels as well. `/unlock`
takes off only what the lock added, so a channel that was read only before stays read only
after. Advanced Security adds locking dangerous role permissions and a single full lockdown
of everything at once.

`/quarantine` takes away a member's roles and hides every channel from them, without kicking
them. The roles they held are stored with the case, so `/unquarantine` gives them back even
after a restart. Run `/security setup` once to create the role and hide every channel
from it.

## Verification

Verification now has three methods: the web check on supervisor.gg behind a Cloudflare
challenge, a captcha image solved inside Discord, or a single button. You can verify only
suspicious accounts (new or without an avatar) and let everyone else straight in, and set a
time limit after which unverified members are removed. Captcha colours, noise and how fast a
code expires are Advanced Security options.

## Moderation commands and cases

Supervisor's actions used to be Delete, Timeout and Warn. It now has the full set:

- `/ban` (permanent or for a set time, by ID for users not in the server), `/unban`, `/kick`
- `/timeout`, `/untimeout`, `/warn`
- `/purge` with filters for one member, bots, links, attachments, embeds, mentions,
  members with no roles, or text it contains
- `/slowmode`, `/sanitize` for fancy or hoisted nicknames
- `/quarantine`, `/unquarantine`, `/lock`, `/unlock`, `/verify`
- `/note` for private moderator notes, `/cases` and `/case`
- `/backup` (Advanced Security), and `/security status` to see what is on and what permissions are missing

Every action, by a moderator or by an automatic system, is a numbered case you can search by
member, moderator or type. **Warn thresholds** act automatically when a member collects a set
number of warns, and warns expire after 30 days unless you change it.

## Backups

With Advanced Security, Supervisor backs up your channels, roles, permission overwrites and
server settings every three hours and keeps the latest ten. `/backup load` recreates
anything missing and resets anything changed, and can optionally remove channels and roles
the backup does not have. Messages and members' role assignments are not part of a backup.

## What it does not do yet

Being straight about the gaps: there is no appeals site, no way for members to report
messages, no message edit and delete logging, and no panel for Discord's own AutoMod rules.
If you depend on those, a dedicated security bot still has something to offer.

## Getting started

1. Open your server on the [dashboard](https://supervisor.gg/dashboard/integrations/discord)
   and find the Security section.
2. Run `/security status` in your server. It lists the permissions Supervisor is missing and warns
   you if its role is too low to act on your staff. Drag Supervisor's role near the top.
3. Run `/security setup` to create the quarantine role.
4. Add your trusted users, switch on anti-nuke, the join gate and heat, and save.

If you have not added Supervisor yet, [invite it to your server](https://invite.supervisor.gg).
