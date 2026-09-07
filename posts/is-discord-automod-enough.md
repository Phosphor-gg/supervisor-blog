---
title: "Is Discord AutoMod enough for your server?"
date: 2026-08-29
description: "AutoMod is free, native and genuinely good at what it does. Whether it is enough depends on what your server actually struggles with. Here is an honest answer, sourced from Discord's own documentation."
---

# Is Discord AutoMod enough for your server?

**Bottom line:** for a lot of servers, yes, and those servers should not pay anyone. AutoMod is
enough if your problem is a list of words, your community is mostly English speaking, and nobody is
actively evading your filters. It is not enough once harm is contextual, multilingual, or arriving
as images, and that is the gap Supervisor was built for at £13.99 a month.

We make an AI moderation tool, so treat this as an interested party's assessment. Everything
below about AutoMod comes from Discord's own documentation, and we have said where it comes
from so you can check it yourself.

For others it is not close, and the gap is predictable rather than mysterious. This post is about
how to tell which one you are.

## What AutoMod is

AutoMod is a set of content filters built into Discord, configured at Server Settings >
AutoMod. Per Discord's AutoMod FAQ, it is "currently available for all servers", so you do not
need a Community server to use it, and it costs nothing.

It gives you two groups of filters. **Keyword Filters** covers the **Commonly Flagged Words
Rule**, which switches on Discord's ready-made lists in three categories (**Insults and
Slurs**, **Sexual Content** and **Severe Profanity**), and the **Custom Keywords Rule**, where
you build your own list. **Spam Filters** covers the **Block Spam Content Rule**, aimed at
unsolicited advertising and invite spam, and the **Block Mention Spam Rule**, which caps how
many mentions one message may contain.

When a filter matches, AutoMod can block the message before it is posted, send an alert to a
private channel, time the member out, or block that member from using text, voice and other
interactions. You can exempt roles and channels, and exempting a channel also exempts its
threads and text chat in voice.

## What AutoMod does genuinely well

This is the part most comparison posts skip, so it goes first.

**It blocks before the message posts.** AutoMod runs inside Discord, so a blocked message never
appears in the channel. No bot can do this. A bot, ours included, sees a message after it has
been posted and then deletes it, which always leaves a window where members can read it. If
your requirement is that a specific word never reaches the channel, AutoMod is not just
adequate, it is the only correct tool.

**It costs nothing and adds no dependency.** No bot to invite, no third party holding Manage
Messages in your server, no service to go down, no bill. For a huge number of servers that
alone settles the question.

**The ready-made lists are a real head start.** Discord's three categories cover the most
common problems without you writing anything, and you can exempt individual words your
community uses normally.

**It is honest about its own limits.** Discord's documentation says the spam filter is "powered
by machine learning that is informed by spammy messages users have previously reported to us"
and that it "is not perfect so it might not catch everything that you may consider spam". That
is a more candid description than most paid products give.

**The exemption model is well designed.** Per-role and per-channel exemptions that cascade to
threads and text-in-voice is a thoughtful piece of engineering, and it is the thing that makes
aggressive filters survivable in a real community.

## Where AutoMod runs out

Four limits, all of them properties of the mechanism rather than faults.

**The built-in categories cover three things.** Insults and slurs, sexual content, severe
profanity. That is the complete list of what AutoMod classifies for you. There is no built-in
category for harassment, threats, scams, or self-harm. Anything in those areas becomes a
keyword list you write and maintain, and Discord's API documentation caps you at **six keyword
rules per server**.

**A word list only catches what you wrote down, spelled the way you wrote it.** Anyone trying
to get past a filter does not type the listed word. They type `fr33 n1tr0`, or `h8`, or
`s.c.a.m`, or they use Cyrillic characters that look identical to Latin ones, or they insert
invisible characters mid-word. Regex helps, and you get up to 10 patterns per rule, but a
pattern loose enough to catch the variations is usually loose enough to catch innocent
messages too, and it is a maintenance job with no end.

**The ready-made lists and the spam filter are English only.** From Discord's FAQ directly:
"AutoMod can detect words and phrases in any language from your Custom Keyword Rules. However,
the word lists of Commonly Flagged Words, as well as the Spam Content filter, are currently
only available in English." If your community speaks anything else, that language is entirely
your own keyword list, inside those six rules.

**Every filter judges one message on its own.** Nothing in AutoMod's rule set weighs the
conversation a message sits in. So the messages that most need judgement are the ones it
cannot make: "do it then", "nobody would miss you", "stop pretending". Harmless in one thread,
serious in another, identical as strings.

There is also no documented image or video filter. Every rule type Discord documents operates
on message text, keywords, mentions or profile text.

## So is it enough? A straight answer

**AutoMod is enough if:**

- Your moderation problem is a list of words and links you do not want posted.
- Your community is mostly English speaking.
- Your active human moderators can handle the judgement calls that filters cannot.
- Nobody is systematically trying to evade your filters.

That describes most small and medium servers, and if it describes yours, turn AutoMod on,
spend an hour on your keyword rules, and stop there. Paying for moderation you do not need is
a bad trade.

**AutoMod is not enough if:**

- The harm in your server is contextual: harassment campaigns, grooming, coordinated
  targeting of one member, threats phrased carefully.
- People are actively evading your word lists, and the same content keeps arriving in new
  spellings.
- Your community is multilingual.
- Harmful content arrives as images or video.
- Your moderators are spending real hours on word lists and appeals, and the false positives
  are annoying legitimate members.

None of those are volume problems or spelling problems, and none of them are solved by
a longer list.

## Where Supervisor fits, and where it does not

Supervisor is an AI moderation bot. Instead of matching strings, it reads what a message means,
which is why the evasion tricks have nothing to work on. It classifies across 16 labels rather
than three categories, covering harassment, hate, threats, scams, spam, self-harm and illegal
activity among others. It can weigh recent conversation history when a message is ambiguous on
its own, it moderates images and video, and it works in over 100 languages without a keyword
list per language.

It is also genuinely narrower than AutoMod in several ways, and you should know that before
installing anything:

- **It deletes after the message posts.** It cannot block beforehand. AutoMod wins here and
  always will.
- **It does not scan member profiles**, which AutoMod does.
- **It has no raid protection**, no anti-nuke, no verification gate and no captcha.
- **Its actions are Delete, Timeout and Warn.** No ban, no kick.
- **It has no utility features at all.** Three slash commands, and everything else is
  configured on the web dashboard.
- **It costs money**: £13.99 a month, or about £4.99 a month on the three year cycle, with a
  seven day trial and £0.25 of moderation free on signup.

Which is why the sensible setup for most servers is both. Leave AutoMod on for the strings you
never want posted, and add an AI layer for the meaning it cannot read. There is a
[full comparison of the two approaches](/blog/supervisor-vs-discord-automod) and a
[breakdown of what each one costs](/blog/discord-automod-pricing) if you want the detail.

## For developers and platforms

AutoMod is a Discord feature and does not exist outside Discord, so if you are moderating your
own product none of this applies to you. Supervisor has a REST API with SDKs for Python,
JavaScript, Go, Rust and Java, and a Platform API for provisioning moderation to your own
users. The [API reference](https://supervisor.gg/docs/integrations/api) has the endpoints.

The fastest way to answer the question in the title is to test it on your own content. Paste a
message that gets past your keyword rules into the [live demo](https://supervisor.gg/demo) and
see whether it gets caught, or [add Supervisor to your server](https://invite.supervisor.gg).
