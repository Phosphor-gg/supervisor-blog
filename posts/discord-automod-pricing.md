---
title: "Discord AutoMod pricing: it is free, and here is what that covers"
date: 2026-08-29
description: "Discord AutoMod costs nothing and there is no premium tier. The useful question is what free covers, where it stops, and what closing that gap costs, so here are both sides with real numbers."
---

# Discord AutoMod pricing: it is free, and here is what that covers

AutoMod is free. There is no premium tier, no paid unlock, no per server fee and nothing to
buy. It is a feature of Discord itself, available in every server, and if you have not turned
it on you are leaving free moderation on the table.

So a pricing post about AutoMod is really a post about two other questions: what does free
get you, and what does it cost to cover what free does not reach. Here are both, with the
numbers from each side.

## What free gets you

Per Discord's own developer documentation, AutoMod gives every server five kinds of rule,
each capped:

| Rule type | What it checks | How many per server |
| --- | --- | --- |
| Keyword | words from a list you write, plus regex | **6** |
| Keyword preset | Discord's own internal wordsets | 1 |
| Spam | content that "represents generic spam" | 1 |
| Mention spam | more unique mentions than your limit, up to 50 | 1 |
| Member profile | words from your list, in a member's profile | 1 |

Each keyword rule holds up to 1,000 keywords of 60 characters or less, and up to 10 regular
expression patterns of 260 characters or less. When a rule matches, AutoMod can block the
message so it never posts, log it to a channel, time the member out, or block that member
from using text, voice and other interactions.

For zero pounds, that is a lot. The block action in particular does something no bot can do,
because AutoMod runs inside Discord and stops the message before it appears. A bot sees a
message after it has posted and deletes it, which always leaves a window.

## Where free stops

Four things, all of them properties of how the rules work rather than complaints about
them.

**The built-in categories are profanity, sexual content and slurs.** Three, and that is the
complete list. There is no built-in category for harassment, threats, scams or self-harm, so
anything in those areas is a keyword list you write and maintain yourself, inside a budget of
six rules.

**Every rule judges one message on its own.** Nothing in the rule set weighs the conversation
a message sits in, so the messages that need context are the ones it cannot judge.

**The ready-made word lists and the spam filter are English only.** Discord's own AutoMod FAQ
says so: custom keyword rules work "in any language", but "the word lists of Commonly Flagged
Words, as well as the Spam Content filter, are currently only available in English". Every
other language is a keyword list you write and maintain yourself, inside a budget of six
rules.

**There is no documented image or video filter.** Every documented rule type works on
message text, keywords, mentions or profile text.

If your moderation problem is a list of words you never want posted, free covers it
completely and you should stop reading here. If your problem is harassment spelled to dodge
the list, scams, implied threats, or harmful images, free does not reach it, and the rest of
this post is the cost of the part that does.

## What Supervisor costs

Supervisor is a paid AI moderation bot. One plan, every feature in it:

| Billing cycle | Price | Works out at |
| --- | --- | --- |
| Monthly | £13.99 | £13.99 a month |
| Annual | £83.85 | about £6.99 a month |
| Three years | £179.65 | about £4.99 a month |

Every cycle includes **£120 of moderation a month**, and the plan is **per account, not per
server**. One subscription covers any number of servers, which all draw on that same monthly
allowance, so running five communities means one subscription rather than five, shared between
them rather than multiplied.

There is a **seven day free trial** on the monthly and annual cycles, and every new account
gets **£0.25 of moderation free on signup** with no card, which is enough to point the bot at
a channel and watch it work before deciding anything.

## What that works out to per message

Text is billed by the size of the message and the model you pick, so the honest way to answer
"what will this cost me" is to do the arithmetic with the assumption stated out loud.

Assume an average message of 100 bytes, which is roughly a short sentence. The £120 of
moderation included every month covers about:

| Model | Messages a month, at 100 bytes each |
| --- | --- |
| Observer | about 900,000 |
| Sentinel | about 450,000 |
| Arbiter | about 225,000 |

Your own average will differ, and longer messages cost proportionally more, which is why the
assumption is written down rather than hidden. Two things push the real figure further:
batched requests get 50% off, and an identical repeated request inside the cache window is
free. Link filtering and word filtering run before the AI models, so anything they block
costs nothing at all.

For most servers the practical answer is that the included allowance is not the constraint.
At 900,000 messages a month on Observer, a server would need to be posting roughly 30,000
messages a day to exhaust it.

## Which is cheaper for you

Honestly:

- **If AutoMod's three presets and six keyword rules cover what your server struggles with,
  free is cheaper and better.** Nothing beats free and native. Do not pay for a problem you
  do not have.
- **If you are running several servers**, note the shape of the difference rather than just
  the price. AutoMod is free in every server. Supervisor is one price for your whole account,
  with the allowance shared across them, so the more communities you run the better that ratio
  gets, right up until their combined traffic is what exhausts the allowance.
- **If the content hurting your community is not a string**, free does not have a price
  advantage, because it is not covering the problem at any price. That is the case where
  £13.99 a month, or £4.99 on the long cycle, buys something AutoMod does not sell.

The two are not mutually exclusive and most servers should run both. AutoMod costs nothing
and stops listed words before they post. Supervisor reads what the remaining messages mean.
There is a [full comparison of the two approaches](/blog/supervisor-vs-discord-automod) if
you want the mechanism rather than the money.

## For developers and platforms

AutoMod is a Discord feature, so it does not exist outside Discord. If you are moderating
your own product, Supervisor bills the same way there: per byte at the model rate, through a
REST API with SDKs for Python, JavaScript, Go, Rust and Java. The
[API reference](https://supervisor.gg/docs/integrations/api) has the current rates, and the
[pricing page](https://supervisor.gg/pricing) has the plan.

Want to see what the paid layer catches that a keyword rule does not? Paste a message that
gets past a keyword filter into the [live demo](https://supervisor.gg/demo) and watch it get
caught, or [add Supervisor to your server](https://invite.supervisor.gg).
