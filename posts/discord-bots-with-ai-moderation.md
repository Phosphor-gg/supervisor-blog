---
title: "Which Discord bots actually use AI moderation in 2026"
date: 2026-09-06
description: "Plenty of Discord bots say AI. Far fewer classify what a message means. Here is an audit of seven, sorted into real AI classification, partial machine learning, and rule engines wearing the label."
---

# Which Discord bots actually use AI moderation in 2026

**Bottom line:** of the seven most-used moderation tools on Discord, only **two** classify what a
message means with a model: **Sapphire** and **Supervisor**. **Discord AutoMod** uses machine
learning for one filter, its spam rule. The other four, **MEE6**, **Dyno**, **Carl-bot** and
**Wick**, are rule engines and their documentation does not claim otherwise.

"AI moderation" has become a phrase people put on landing pages, so this post audits the actual
documented mechanism of each one rather than the marketing. We make Supervisor, which is one of
the two, so read the sourcing section at the end before taking our word for any of it.

## The audit at a glance

| Bot | Mechanism | Classifies meaning | Categories | Languages |
| --- | --- | --- | --- | --- |
| Supervisor | AI models | **Yes** | 16 labels | Over 100 |
| Sapphire | AI models | **Yes** | 4 categories | English and German fully |
| Discord AutoMod | Word lists plus ML on spam | Partly | 3 preset lists | Preset lists English only |
| MEE6 | Rule checks | No | None | Word lists you write |
| Dyno | Rule filters | No | None | Word lists you write |
| Carl-bot | Rule modules | No | None | Word lists you write |
| Wick | Rate scoring | No | None | Blacklists you write |

## Real AI classification

### Sapphire

Sapphire's Auto Moderation module includes a genuine AI component, and it is free, which makes it
the most interesting entry in this list. It flags **insults, threats, identity attacks and other
offensive language**, with sensitivity set per category to low, medium or high.

Two documented limits define its scope. Sapphire's own docs state it "only scans 10 messages per
server per minute" without its paid Limit Increase plan, so on a busy server most messages never
reach the model. And "AI Moderation currently fully supports English and German", with other
languages supported but without categorisation of inappropriate language.

Sapphire also does something no other bot here does: it attaches additional actions to the Discord
AutoMod rules you have already configured, rather than ignoring them.

**Verdict:** real AI, four categories, throughput-limited, free.

### Supervisor

This is ours, so weigh it accordingly. Supervisor classifies across **16 labels**, covering
harassment, hate, threats, insults, scams, spam, promotional content, sexual content in three
degrees, self-harm, medical, violence, sensitive content and illegal activity. It weighs recent
conversation history when a message is ambiguous alone, has implicit moderation for harm that is
implied rather than stated, reads images and video rather than counting them, and works in over
100 languages. There is no per-minute scan cap; the constraint is a monthly allowance.

It is also the narrowest product in this list. Three slash commands, no bans or kicks, no raid
protection, no utility features, and £13.99 a month with no free tier for new accounts.

**Verdict:** real AI, widest coverage, paid, narrow product.

## Partial machine learning

### Discord AutoMod

AutoMod is mostly word lists, and it is honest about the one place it uses machine learning. Its
**Block Spam Content Rule** is, in Discord's own words, "powered by machine learning that is
informed by spammy messages users have previously reported to us", with the caveat that the filter
"is not perfect so it might not catch everything that you may consider spam".

The **Commonly Flagged Words Rule** switches on Discord's internal wordsets in three categories,
Insults and Slurs, Sexual Content and Severe Profanity. Discord describes those as ready-made word
lists rather than as classification, and they are English only.

So AutoMod belongs in this list for its spam filter, not for its keyword rules. It also has the one
capability nothing else here can match: it blocks a message before it is posted.

**Verdict:** ML on spam, word lists elsewhere, free and native.

## Rule engines, and that is fine

None of the four below document AI classification of message content, and none of them claim to.
They are listed here because people ask, and because a rule engine is the correct tool for
countable problems.

### MEE6

The Moderator plugin's automod is eight checks: Bad Words, Repeated Text, Server Invites, External
Links, Excessive Caps, a combined Excessive Emojis, Spoilers and Mentions check, Zalgo, and
Anti-Spam. All string matches or counters.

Worth a note for accuracy: MEE6 markets **MEE6 AI** as a separate product built on ChatGPT and
Dall-E. We did not read that product's documentation, so we are making no claim about what it does.
What we can say is that the moderation checks documented in the Moderator plugin are rules.

### Dyno

Nineteen filters, more than anyone else here, covering everything from Fast Message Spam and Mass
Mentions to Known Phishing Links, Zalgo Text and Sticker Cooldown. Its Banned Words setting offers
exact or wildcard matching, which is the clearest illustration in this list of what a word list can
and cannot do: exact mode misses `fr33 n1tr0`, and wildcard mode banning "hi" also matches "high".

### Carl-bot

Eight modules: message spam, attachment spam, bad words, caps limit, honeypot, invites, links and
mentions. Its strength is the response rather than the detection, with eleven punishments that
combine in one rule and a `defer` action that routes ambiguous cases to a moderator vote.

### Wick

Wick's Heat system is adaptive, which is why people sometimes assume it is AI. It is not
classification. Heat accumulates from message repetition, emojis, characters, new lines, mentions,
attachments, blacklisted words and links, advertisement and known malicious sites, then decays over
time. Wick describes it as "an adaptive algorithm that adjusts to the user's current actions". It
measures rate and behaviour, not meaning.

## Why the distinction matters

A rule engine and a classifier fail differently, and it is worth knowing which failure you are
buying.

**Rules fail on spelling.** Anything not written down, or written differently, walks past. That is
`fr33 n1tr0`, `h a t e`, Cyrillic look-alikes, zero-width characters, and every language you did
not write a list for.

**Rules fail on the single message.** Counters ask how many and never what, so one calmly written
threat or scam trips nothing.

**Classifiers fail differently.** They can be wrong about tone, they cost money or throughput, and
they need a sensitivity setting you have to tune. What they do not do is miss a message purely
because it was spelled creatively.

For most servers the practical answer is both: a rule engine for the countable work, and a
classifier for meaning.

## Why trust this audit

Every mechanism above was read from the vendor's own documentation on 29 August 2026: Discord's
auto moderation developer documentation and its AutoMod FAQ, last updated 15 June 2026;
docs.sapph.xyz for Sapphire's AI categories, scan limit and language support, all quoted directly;
wiki.mee6.xyz for MEE6's Moderator plugin; Dyno's automod documentation; docs.carl.gg; and
docs.wickbot.com for Wick's Heat model. Where we did not read something, as with MEE6 AI, we have
said so rather than guessed.

We make Supervisor, so this is not a neutral audit. What we have done instead is publish the
mechanism for every product including our own, list our limits next to our capabilities, and give
you the sources so you can check any line of it.

On our own side the numbers come from our evaluation set rather than marketing. Supervisor's models
are retrained on real moderation feedback, the thumbs up and thumbs down votes people leave on live
flags in their own servers. The last full retrain moved average F1 across the 16 labels from 0.794
to 0.941 on our internal evaluation set, with errors on harmless messages down 44 percent, and
version 2.2 improved macro-F1 again across all three model tiers. The method and per-label figures
are in the [2.1 release post](/blog/supervisor-2-1).

We have no customer reviews or ratings to show you, because we have not collected any.

## So which should you use?

- **Free, and your server is English or German speaking and not especially busy:** Sapphire, whose
  AI moderation costs nothing. Turn Discord AutoMod on underneath it.
- **You want more categories, more languages, images and video, and every message seen:** that is
  what Supervisor sells, and we would rather you tried it on your own content than took our word.
- **Your problems are countable:** a rule engine is the right tool and cheaper. Dyno has the most
  filters, Carl-bot the best responses.

There is a fuller roundup of the [best Discord moderation bots](/blog/best-discord-moderation-bots-2026)
if you want the category rather than the AI question, and a
[head-to-head with Sapphire](/blog/supervisor-vs-sapphire-moderation), the only other real AI
option here.

Want to see what a classifier catches that a keyword rule does not? Paste a message that gets past
your current filters into the [live demo](https://supervisor.gg/demo), or
[add Supervisor to your server](https://invite.supervisor.gg).
