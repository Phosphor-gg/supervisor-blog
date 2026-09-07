---
title: "MEE6 review: what it is good at and where it runs out"
date: 2026-08-29
description: "An honest review of MEE6 from a company that makes a competing moderation tool. What its automod and enforcement actually cover, what its 7,217 Trustpilot reviews say, and where a rule engine stops."
---

# MEE6 review: what it is good at and where it runs out

**Bottom line:** MEE6 is a strong all-in-one with the best enforcement ladder in this category and
an audit log to match, and its moderation is free. Its eight automod checks are string matches and
counters, so they miss the calmly written message that trips nothing. Run MEE6 for breadth and
enforcement, and add Supervisor for the meaning those checks cannot read.

We make an AI moderation tool, so treat this as an interested party's assessment. Every claim
about MEE6 below comes from MEE6's own documentation and pricing page, and the ratings come from
a public page you can open yourself. Where we could not verify something, we say so instead of
guessing.

## What MEE6 is

MEE6 is an all-in-one Discord bot, and by its own account on its pricing page it is "trusted and
used by more than 21 Million servers". It covers moderation, levels, social alerts across Twitch,
X, YouTube, RSS, Reddit and Instagram, giveaways, birthdays, economy, and a bot personaliser that
changes the bot's avatar, name and activity. It is configured entirely through a web dashboard,
and it markets MEE6 AI as a separate product built on ChatGPT and Dall-E.

Premium is priced per server. In MEE6's own words: "MEE6 Premium applies to a single server. To
use Premium on multiple servers, you'll need a separate subscription for each."

## What MEE6 does well

**The enforcement ladder is the best part.** Automated actions escalate on how many warnings a
member accumulates inside a time window, applying the first matching rule and ordered by
severity. MEE6's own examples are ten warnings in fourteen days for a permanent ban, five in seven
days for a three-day ban, and two in twenty four hours for a one-day mute. That is a real,
graduated policy rather than a single blunt response, and it is more than many moderation tools
offer, ours included.

**Moderators get proper tools.** `/ban`, `/tempban`, `/kick`, `/clear` for up to 50,000 messages,
an infractions record per member, and `/clear-all-infractions` for a reset. Immunity roles keep
staff out of the automod's way.

**The audit log is thorough.** Around two dozen event types, from message edits and deletions
through role changes, bans, unbans, voice channel joins and channel creation, delivered by
webhook every one to five minutes. If you need to reconstruct what happened during an incident,
that is the feature that does it.

**The automod checks are sensibly scoped.** Each of the eight checks takes its own action setting
and its own role and channel rules, using "deny for all roles except" and "allow for all channels
except" patterns. That granularity is what makes an aggressive filter survivable in a real
community.

**The commercial terms are fair.** Every plan is fully refundable for seven days, and a
subscription is transferable to another server, which matters more than it sounds given the per
server licensing. You can cancel any time and keep access until the period ends.

**Breadth is a genuine feature.** For a server that wants one bot doing ten jobs, MEE6 is a
reasonable answer, and that is why it is on so many servers.

## Where MEE6 runs out

The automod ruleset is eight checks: Bad Words, Repeated Text, Server Invites, External Links,
Excessive Caps at a default 70% threshold, a combined Excessive Emojis, Spoilers and Mentions
check, Zalgo, and a separate Anti-Spam feature watching message frequency.

Every one of them is a string match or a counter, and that is the ceiling.

**Bad Words only catches what you wrote down.** Not the leetspeak version, not the homoglyph
version, not the one with an invisible character in the middle, and not the same idea in another
language.

**Counters measure volume, not meaning.** A targeted threat or a well-written scam is one calm,
correctly spelled message. It trips no counter and matches no list.

**There are no harm categories.** Nothing in the eight checks identifies harassment, hate,
threats, self-harm or scams as categories in their own right, so each of those becomes a word
list you maintain.

**Nothing weighs conversation context**, so ambiguous messages are judged alone.

**The plugin documentation describes no image or video moderation.** The checks operate on
message text, links, mentions and formatting.

None of that makes MEE6 a bad tool. It makes it a rule engine attached to a very good enforcement
system, which is what it says it is.

## What users say

MEE6 is the only one of the major Discord bots we looked at that publishes no aggregate rating on
top.gg, so there is no second source to cross-check against. What it does have is a large
Trustpilot profile.

| Source | Score | Sample | Checked |
| --- | --- | --- | --- |
| Trustpilot | 4.8 out of 5 | 7,217 reviews | 29 August 2026 |

The distribution is 85% five star, 8% four, 2% three, under 1% two, and 4% one star. The profile
is claimed by MEE6.

Two caveats belong next to that number, both of them Trustpilot's own. The profile carries the
notice "No recent history of asking for reviews. This company hasn't invited customers recently,
so reviews may not be representative", and Trustpilot also flags that the company has not replied
to negative reviews.

We want to be straight about something here, because it would be easy to do the opposite. MEE6
has a well-known reputation in Discord communities for putting a lot behind its paywall, and we
could have written a section built entirely around that. But its own rating, on more than seven
thousand reviews, is 4.8 out of 5. Both of those things are true, we could not systematically
sample the complaint side from sources we can cite, and publishing only the half that suits us
would not be a review.

## Where Supervisor fills the gaps, and where it does not

Supervisor is an AI moderation bot. Instead of matching strings and counting events, it reads what
a message means:

- No word list to spell around, so leetspeak, homoglyphs and invisible characters are read as
  what they mean.
- 16 labels including harassment, hate, threats, scams, self-harm and illegal activity, which is
  the category coverage eight checks do not provide.
- Conversation context weighed when a message is ambiguous alone.
- Images and video moderated, not just counted.
- Over 100 languages without a word list per language.

Where it does not fill the gap, plainly:

- **Supervisor cannot ban or kick.** Delete, Timeout and Warn are the whole list. MEE6's
  escalation ladder has no equivalent here, and if graduated enforcement is what you need, MEE6
  does it and we do not.
- **Supervisor has no audit log**, only an alerts channel.
- **Supervisor has no counters.** Caps percentage, emoji counts, repeated text and message
  frequency are not things it measures.
- **Supervisor has no utility features.** Three slash commands, no levels, no social alerts, no
  economy, no giveaways.
- **Supervisor has no lifetime plan and no free tier for new accounts**, just a seven day trial
  and £0.25 of moderation free on signup.

There is a [full comparison of the two approaches](/blog/supervisor-vs-mee6-moderation) if you
want the mechanism in depth, and a breakdown of [what MEE6 costs](/blog/mee6-pricing) including
which headline rate actually renews.

## Who MEE6 is right for

MEE6 is right for you if you want one bot covering many jobs, if you want a proper enforcement
ladder with bans and infraction history, if you want an audit trail, and if your moderation
problems are countable or matchable. For a very large number of servers that is an accurate
description, and its moderation works without paying.

It is not sufficient on its own if the content actually hurting your community is contextual,
multilingual, image-based, or written by someone deliberately spelling around your filters. That
is not a criticism of MEE6 so much as a description of what rule engines are for. Running both is
the normal answer.

## For developers and platforms

MEE6 is a Discord bot, so it does not help you moderate your own product. Supervisor has a REST
API with SDKs for Python, JavaScript, Go, Rust and Java, plus a Platform API. The
[API reference](https://supervisor.gg/docs/integrations/api) has the endpoints.

The quickest way to judge any of this is on your own content. Paste a message that gets past a
keyword filter into the [live demo](https://supervisor.gg/demo) and see whether it gets caught,
or [add Supervisor to your server](https://invite.supervisor.gg).
