---
title: "Supervisor vs collony.ai: AI moderation for Discord compared"
date: 2026-11-16
description: "collony.ai is an AI community manager for Telegram and Discord that answers questions as well as moderating. Supervisor is AI moderation plus a free security suite. An honest comparison of coverage, price, privacy and what each does that the other does not."
---

# Supervisor vs collony.ai: AI moderation for Discord compared

**Bottom line:** if your community is on Discord and the job is moderation, Supervisor covers
more for less. It classifies 16 harm labels in over 100 languages, reads images and video,
includes a free security suite (anti-nuke, join gate, spam filtering, lockdown, verification),
and Premium at £13.99 a month includes enough moderation for roughly 900,000 messages across any
number of servers. collony.ai's Protect plan is $29 a month for 500 AI-checked messages a day on
one platform. Pick collony.ai instead if you need Telegram, want a bot that answers member
questions from your docs, or want rules written in plain English.

collony.ai is one of the newer AI tools in this space, and it is a well thought out one. It is
worth being precise about what it is, because it is not quite the same kind of product as
Supervisor.

## Quick comparison

| | collony.ai | Supervisor |
| --- | --- | --- |
| Platforms | Telegram and Discord (one on Free and Protect) | Discord, plus a REST API for anything else |
| How it decides | An AI reads your plain-language rules and presets | **Purpose-built classifiers, 16 labels** |
| Who runs the AI | AI providers such as OpenAI, per its privacy policy | **Our own self-hosted models** |
| Languages | Bot menus in 9 languages; replies in the member's language | **Over 100 languages moderated** |
| Images | Images on by default; GIFs, video and stickers optional | Images and video |
| Security suite (anti-nuke, join gate, verification) | Surge Guard, flood limits, impersonation checks | **Anti-nuke, join gate, Heat, lockdown, quarantine, verification, free** |
| Answers member questions | **Yes, from your knowledge base (Grow)** | No |
| Sentiment insights | **Yes (Grow)** | No |
| Message storage | Searchable chat history, logs kept typically up to 90 days | **Message text not stored** |
| Developer API | No public API; MCP for managing it from AI apps | **REST API and five SDKs** |
| Entry price for AI moderation | $29 a month, 500 messages a day | **£13.99 a month, about 900,000 messages a month** |

## What collony.ai actually is

collony.ai describes itself as AI community moderation for Telegram and Discord, and its
documentation shows a product built in layers. Every message passes them in order, and the first
one that acts decides what happens:

1. **Surge Guard** watches the message rate per channel and turns on slow mode during a flood or
   raid, then lifts it when things calm down.
2. **Impersonation protection** catches members copying the name, handle or profile picture of
   someone on your team, including look-alike letters and mirrored or cropped pictures. Its docs
   note no AI is involved in this layer.
3. **Blocklists** for words, phrases and domains, handled instantly.
4. **AI rules**: everything left is read by an AI using your community rules, written in plain
   language, plus ten ready-made presets for things like phishing, wallet-address spam, DM
   solicitation and "thirst-trap" bots.

The plain-language rules are the clever part. You paste something like "INSTANT BAN: anyone
offering to DM, help, verify or sync anything on the team's behalf" and the AI enforces it. For
crypto and Web3 communities, where scams change weekly, that is a real advantage.

On the Grow plan it becomes more than a moderator: it answers member questions from your
knowledge base, posts on a schedule, tracks sentiment and topics, and can be run from Claude,
ChatGPT or Cursor through MCP.

## Where collony.ai's approach runs out

**It is priced by the message, and the allowance is small.** Protect includes 500 security
credits a day, and its billing docs say one credit is one message checked. That is about 15,000
messages a month, on one platform, for $29. A busy Discord server passes that in an afternoon.
The docs say protection never stops when credits run out, but they do not say how messages
beyond the allowance are checked, so we will not guess.

**The AI is someone else's.** collony.ai's privacy policy lists "AI service providers (e.g.
OpenAI)" as sub-processors for moderation and response generation, and says some sub-processors
may process data outside the European Economic Area. That is a normal setup for a young product,
but it means your members' messages leave collony.ai to be judged.

**It keeps your messages.** Its Chat History is a searchable feed of every message the bot has
seen, with an all-time range and CSV export. The privacy policy says community messages are kept
within the log retention period, typically up to 90 days. Useful for review, but it is a lot of
member data to hold.

**A rules engine is only as good as the rules.** An AI reading your plain-language rules is
flexible, but the categories are whatever you and the presets describe. There is no fixed,
measured set of harm labels you can check its accuracy against.

**Discord security is thin.** Surge Guard and impersonation checks are useful, but there is no
anti-nuke, no join gate on account age, no verification and no backups in its docs. If a
moderator account is compromised, nothing is watching the audit log.

## What Supervisor does differently

**Purpose-built models, run by us.** Supervisor does not send your messages to a general-purpose
chatbot. It runs its own classifiers on its own hardware, trained for one job: reading what a
message means. It catches leetspeak, homoglyphs and creative spelling, weighs conversation context
when a message is ambiguous, and classifies across 16 labels including harassment, hate, threats,
scams, spam, sexual content and self-harm. Message text is processed in memory and not stored.

**Over 100 languages.** Messages in other languages are translated by a self-hosted model and then
classified, with no separate rule set per language.

**Images and video.** Supervisor reads what is in the picture, not just whether one was posted.

**A full security suite, free.** Anti-nuke watching the audit log, a join gate for account age,
missing avatars and harmful usernames, Heat spam filtering, auto lockdown, quarantine,
verification and numbered moderation cases. It never touches the AI models, so it costs nothing
and keeps working even with no credits. Panic mode, join raid detection and automatic backups are
in Premium.

**Billed by size, not by message count.** Premium is £13.99 a month, £6.99 a month billed
annually, or £4.99 a month over three years, and every cycle includes £120 of moderation. At an
average message of 100 bytes that covers roughly 900,000 messages a month on the Observer model,
and one subscription covers every server you run.

**An API.** If your community is not on Discord, the same models are available through a REST API
with SDKs for Python, JavaScript, Go, Rust and Java.

## What collony.ai does that Supervisor does not

- **Telegram.** Supervisor has no Telegram bot today. If your community lives on Telegram,
  collony.ai is the one built for it.
- **Answering questions.** Supervisor moderates; it does not answer members from your docs.
- **Plain-language rules.** Supervisor's labels are fixed and measured. You choose which are on
  and what happens, but you cannot write a new rule in a sentence.
- **Impersonation of your team.** collony.ai compares names and pictures against your staff.
  Supervisor's join gate flags harmful usernames, but does not compare members against your team.
- **Insights, scheduled posts and MCP.**

## Why trust this comparison

Everything above about collony.ai comes from its own material: its homepage, pricing page,
billing, protection, AI rules, enforcement, impersonation, Surge Guard, chat history and settings
documentation, and its privacy policy, all read on 16 November 2026. Its plans and limits may
change, so check its pricing page before you decide.

We make Supervisor, so this is not a neutral comparison. What we have done is put collony.ai's
advantages in their own section, in plain terms, and leave out anything we could not read. The
Supervisor figures come from our own pricing and source code. We have no customer reviews to show
you, so judge it on your own content.

## So which should you use?

If you run a Discord community and want moderation that reads meaning, in any language, with
server security included and without counting messages, use Supervisor.

If you run a Telegram group, or you want one bot that both moderates and answers questions for
your community, collony.ai is built for that and does it well.

Paste a message that gets past a keyword filter into the [live demo](https://supervisor.gg/demo)
and see what Supervisor makes of it, or [add Supervisor to your server](https://invite.supervisor.gg).
