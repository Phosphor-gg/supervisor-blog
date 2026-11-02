---
title: "Wick bot review: what it is good at and where it runs out"
date: 2026-08-29
description: "An honest review of Wick, the Discord security bot, from a company that makes a competing moderation and security bot. What anti-nuke, panic mode and the Heat system actually do, and where a security model stops."
---

# Wick bot review: what it is good at and where it runs out

*Updated 2 November 2026: Supervisor now has its own [security suite](/blog/supervisor-security-suite),
so the sections on Supervisor below have been rewritten. The review of Wick itself is unchanged.*

**Bottom line:** Wick is a security bot, not a moderation bot, and a strong one: anti-nuke, panic
mode, restore, quarantine and verification, with an adaptive Heat system for spam. Its Heat model
measures rate rather than meaning, so a single calm harmful message generates almost none.
Supervisor now covers most of Wick's security features as well as reading what members say, so
for most servers one bot is enough. Wick keeps an edge on appeals, member reports, logging, its
AutoMod panel, the rescue key and track record.

We make Supervisor, an AI moderation bot that now has its own security suite, so treat this as an interested party's assessment. Every claim
about Wick below comes from Wick's own documentation, and the rating comes from a public page you
can open yourself. Where we could not verify something, we say so instead of guessing.

Wick is a **security** bot, and Supervisor started as a **content moderation** bot. Since
Supervisor added a security suite in November 2026 the two overlap a lot more, but understanding
that difference in emphasis is still most of what this review is for.

## What Wick is

Wick protects the structure of a Discord server rather than policing what people say in it. Its
documentation names its **Anti-Nuke system** as "the critical feature that differentiates Wick
from all other Discord Bots", and describes it as a monitoring system watching channel and role
creation and deletion, bans and kicks, and webhook creation and deletion. Its target is not the
ordinary member. It is the rogue admin, the compromised account, and the person who was trusted
with permissions.

Around that sit Panic Mode, a Restore System, Quarantine, Verification, Lockdown, Backups, and a
moderation command set covering Ban, Kick, Purge, Timeout, Sanitize, Slowmode, Notes, Warn, plus
case tracking through Cases, Modcases and Nuke Cases.

## What Wick does well

**Anti-nuke is a category of protection almost nothing else offers.** Most bots moderate members.
Wick watches the people who could destroy the server outright. It treats attempts to bypass
quarantine, to add dangerous permissions to any role, or to change the vanity URL as quarantine
offences in themselves, which closes the obvious escape routes rather than just the front door.

**Panic Mode is properly engineered.** On detecting a nuke attempt, Wick locks the server down and
hands complete authority to the owner and itself. It then deploys a separate "miniWick" to
retrieve pre-attack server state, deliberately isolated so that hundreds of simultaneous nukes do
not degrade the main bot. That is a thoughtful piece of architecture, not a marketing feature.

**The Heat system is a better model than fixed thresholds.** Rather than "five messages in five
seconds", every action contributes heat that decays over time, so a burst of enthusiasm cools off
while sustained abuse accumulates. Wick describes it as "an adaptive algorithm that adjusts to the
user's current actions and scales properly with an increase in members and their activity". Heat
comes from message repetition, emojis, characters, new lines, mentions with `@everyone` weighted
heavily, attachments, inactivity in quiet channels, blacklisted words and links, advertisement,
NSFW websites, and malicious websites including ones carrying IP-grabbers and keyloggers. Auto
Timeouts then escalate, with a multiplier that makes each subsequent punishment harsher so that
raiders cannot simply wait out a fixed cap.

That is a genuinely better answer to spam than a counter, and Wick's claim that it "rarely
generates false positives, unlike conventional methods" is at least mechanically plausible,
because decay means ordinary chatter never accumulates enough.

**The documentation is honest about failure modes.** On the Restore System, Wick writes that
without Imaging enabled restoration "is a finicky process and lacks a lot of information and the
server may not be restored properly". Most products would not tell you that up front.

## Where Wick runs out

Not flaws, just the boundary of what a security model covers.

**Heat measures behaviour, not meaning.** It counts how much, how fast, how repetitive, how many
mentions, how many emojis. It does not ask what a message says. A single calmly written, correctly
spelled message sent at a normal pace generates almost no heat regardless of its content. That is
precisely the shape of a targeted threat, a grooming attempt, or a convincing scam.

**The blacklists are lists.** Words Blacklist and Links Blacklist catch what you wrote down,
spelled the way you wrote it, in the languages you wrote it in. Leetspeak, homoglyphs, spaced-out
text and invisible characters all get past.

**There are no harm categories.** Nothing classifies harassment, hate, threats or self-harm as
categories. The advertisement, NSFW and malicious-website factors are about links, not about what
one member is saying to another.

**Nothing weighs conversation context.** Heat accumulates per user, so a message that is only
harmful given what preceded it looks identical to any other.

## What users say

| Source | Score | Sample | Checked |
| --- | --- | --- | --- |
| top.gg | 84 out of 100 | 259 ratings | 29 August 2026 |

Note that top.gg rates on a 0 to 100 scale rather than out of five, so 84 there is not the same as
8.4 or 4.2 elsewhere. We did not find a Trustpilot profile to cross-check against, and we could
not systematically sample individual reviews from sources we can cite, so rather than characterise
themes we cannot evidence, that aggregate is what we are reporting.

## Where Supervisor fills the gaps, and where it does not

Supervisor reads what a message means rather than measuring rate and matching strings:

- No blacklist to spell around, so leetspeak, homoglyphs and invisible characters are read as what
  they mean.
- 16 labels including harassment, hate, threats, scams, self-harm and illegal activity.
- Conversation context weighed when a message is ambiguous alone.
- Images and video moderated, not just counted as attachments.
- Over 100 languages without a list per language.

Since 2 November 2026 Supervisor also covers most of Wick's own ground. Free for every server,
and using no credits:

- **Anti-nuke** with per-minute and per-hour limits on channel, role, ban, kick and webhook
  actions, quarantine hold, vanity URL protection, public role and channel permission monitoring,
  and a bot addition filter.
- **A join gate**, **Heat** spam filtering (including a public phishing and malware domain list),
  **auto lockdown**, `/lock`, **quarantine** and Cloudflare **verification**.
- **Moderation commands** including `/ban`, `/kick`, `/timeout`, `/warn`, `/purge` and `/note`,
  with numbered cases and warn thresholds.

Panic mode, join raid detection, backups and restore, heat tuning and role or full lockdown are
in Advanced Security, which is included in Supervisor Premium.

Where it still does not fill the gap:

- **No appeals site and no member reports.**
- **No 35-event logger**, so no message edit or delete logs. Supervisor logs its own security and
  moderation actions.
- **No Discord AutoMod panel, no rescue key**, no custom permit levels and no Imaging.
- **Vanity URL protection punishes the change but cannot restore the old URL.**
- **A short track record.** The security suite is new; Wick's has been running for years.

There is a [full comparison of the two approaches](/blog/supervisor-vs-wick-moderation) if you
want the mechanism side in depth.

## Who Wick is right for

Wick is right for you if your risks are structural: raids, nukes, rogue or compromised admins,
alt-account floods, or a need to verify people at the door and put the server back together if
something goes wrong. If you run a large public server where a single compromised moderator
account is a genuine threat, this is the category of tool you need, and Wick is the most focused
one in it.

It is not sufficient on its own if your members are legitimate and the problem is what they are
posting. Heat will catch the flooder and the advertiser. It will not catch the person quietly
making one member's life miserable, because that person is not generating heat.

For most servers, Supervisor now covers both halves in one bot. If you depend on Wick's appeals,
reports, logging or rescue key, running Wick alongside Supervisor's AI moderation still works
well.

## For developers and platforms

Wick is a Discord security bot, so it has no application outside Discord. Supervisor has a REST
API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints.

The quickest way to judge the content side is on your own content. Paste a message that gets past
a keyword filter into the [live demo](https://supervisor.gg/demo) and see whether it gets caught,
or [add Supervisor to your server](https://invite.supervisor.gg).
