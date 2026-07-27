---
title: "Supervisor 2.1: fewer false positives, retrained on your feedback"
date: 2026-07-27
description: "Supervisor 2.1 is a full retrain of all three moderation models, driven by the thumbs-up and thumbs-down votes you left on real flags. Average F1 on our evaluation set goes from 0.794 to 0.941, and errors on harmless messages are down 44 percent."
---

# Supervisor 2.1

Since 2.0 shipped, every flag Supervisor made in Discord came with a 👍 and a 👎 button. Thousands of you pressed them. Those votes are the single most valuable thing we have, because they are not our opinion about whether a decision was right, they are yours, on your own server, about your own members.

We read them. The pattern was uncomfortable and completely fair: Supervisor was too quick to flag. Not missing harmful content, the opposite. It was firing on messages that were obviously fine to a human, and every one of those costs a moderator time and makes the bot feel like a liability.

2.1 is a full retrain of all three models built directly on that feedback.

## What changed

The headline number, on our internal evaluation set, comparing the Arbiter model in 2.0 against the Arbiter model in 2.1. Both are the same base architecture, so this is a like for like comparison:

| | 2.0 | 2.1 |
| --- | --- | --- |
| Average F1 across 16 labels | 0.794 | **0.941** |

Every one of the sixteen labels improved. The largest gains landed on the ones that were weakest before:

<figure style="margin:1.75rem 0;">

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 596 594" width="100%" role="img" aria-label="F1 score per label, Supervisor 2.0 versus 2.1, Arbiter model" style="max-width:596px;height:auto;font-family:system-ui,-apple-system,Segoe UI,sans-serif">
<title>F1 score per label, Supervisor 2.0 versus 2.1 (Arbiter)</title>
<rect x="132" y="16" width="10" height="10" rx="2" fill="#d95926"/>
<text x="148" y="25" fill="#9a9aa4" font-size="12">Supervisor 2.0</text>
<rect x="244" y="16" width="10" height="10" rx="2" fill="#3987e5"/>
<text x="260" y="25" fill="#9a9aa4" font-size="12">Supervisor 2.1</text>
<line x1="132.0" y1="44" x2="132.0" y2="568" stroke="#262a33" stroke-width="1"/>
<text x="132.0" y="584" fill="#9a9aa4" font-size="11" text-anchor="middle">0.00</text>
<line x1="222.0" y1="44" x2="222.0" y2="568" stroke="#262a33" stroke-width="1"/>
<text x="222.0" y="584" fill="#9a9aa4" font-size="11" text-anchor="middle">0.25</text>
<line x1="312.0" y1="44" x2="312.0" y2="568" stroke="#262a33" stroke-width="1"/>
<text x="312.0" y="584" fill="#9a9aa4" font-size="11" text-anchor="middle">0.50</text>
<line x1="402.0" y1="44" x2="402.0" y2="568" stroke="#262a33" stroke-width="1"/>
<text x="402.0" y="584" fill="#9a9aa4" font-size="11" text-anchor="middle">0.75</text>
<line x1="492.0" y1="44" x2="492.0" y2="568" stroke="#262a33" stroke-width="1"/>
<text x="492.0" y="584" fill="#9a9aa4" font-size="11" text-anchor="middle">1.00</text>
<text x="122" y="68" fill="#e6e6ea" font-size="12.5" text-anchor="end">Medical/Injury</text>
<rect x="132" y="54" width="251.4" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="67" width="352.9" height="11" rx="4" fill="#3987e5"/>
<text x="492.9" y="76" fill="#e6e6ea" font-size="11.5" font-weight="600">0.98</text>
<text x="544" y="64" fill="#9a9aa4" font-size="11">+0.28</text>
<text x="122" y="100" fill="#e6e6ea" font-size="12.5" text-anchor="end">Violence</text>
<rect x="132" y="86" width="233.5" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="99" width="319.2" height="11" rx="4" fill="#3987e5"/>
<text x="459.2" y="108" fill="#e6e6ea" font-size="11.5" font-weight="600">0.89</text>
<text x="544" y="96" fill="#9a9aa4" font-size="11">+0.24</text>
<text x="122" y="132" fill="#e6e6ea" font-size="12.5" text-anchor="end">Sexual (Unlawful)</text>
<rect x="132" y="118" width="258.0" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="131" width="334.6" height="11" rx="4" fill="#3987e5"/>
<text x="474.6" y="140" fill="#e6e6ea" font-size="11.5" font-weight="600">0.93</text>
<text x="544" y="128" fill="#9a9aa4" font-size="11">+0.21</text>
<text x="122" y="164" fill="#e6e6ea" font-size="12.5" text-anchor="end">Promotional</text>
<rect x="132" y="150" width="270.8" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="163" width="340.5" height="11" rx="4" fill="#3987e5"/>
<text x="480.5" y="172" fill="#e6e6ea" font-size="11.5" font-weight="600">0.95</text>
<text x="544" y="160" fill="#9a9aa4" font-size="11">+0.19</text>
<text x="122" y="196" fill="#e6e6ea" font-size="12.5" text-anchor="end">Sensitive</text>
<rect x="132" y="182" width="273.8" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="195" width="342.1" height="11" rx="4" fill="#3987e5"/>
<text x="482.1" y="204" fill="#e6e6ea" font-size="11.5" font-weight="600">0.95</text>
<text x="544" y="192" fill="#9a9aa4" font-size="11">+0.19</text>
<text x="122" y="228" fill="#e6e6ea" font-size="12.5" text-anchor="end">Hate/Racism</text>
<rect x="132" y="214" width="275.3" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="227" width="343.5" height="11" rx="4" fill="#3987e5"/>
<text x="483.5" y="236" fill="#e6e6ea" font-size="11.5" font-weight="600">0.95</text>
<text x="544" y="224" fill="#9a9aa4" font-size="11">+0.19</text>
<text x="122" y="260" fill="#e6e6ea" font-size="12.5" text-anchor="end">Spam</text>
<rect x="132" y="246" width="277.8" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="259" width="345.3" height="11" rx="4" fill="#3987e5"/>
<text x="485.3" y="268" fill="#e6e6ea" font-size="11.5" font-weight="600">0.96</text>
<text x="544" y="256" fill="#9a9aa4" font-size="11">+0.19</text>
<text x="122" y="292" fill="#e6e6ea" font-size="12.5" text-anchor="end">Harassment</text>
<rect x="132" y="278" width="266.7" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="291" width="318.7" height="11" rx="4" fill="#3987e5"/>
<text x="458.7" y="300" fill="#e6e6ea" font-size="11.5" font-weight="600">0.89</text>
<text x="544" y="288" fill="#9a9aa4" font-size="11">+0.14</text>
<text x="122" y="324" fill="#e6e6ea" font-size="12.5" text-anchor="end">Illegal</text>
<rect x="132" y="310" width="275.5" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="323" width="322.8" height="11" rx="4" fill="#3987e5"/>
<text x="462.8" y="332" fill="#e6e6ea" font-size="11.5" font-weight="600">0.90</text>
<text x="544" y="320" fill="#9a9aa4" font-size="11">+0.13</text>
<text x="122" y="356" fill="#e6e6ea" font-size="12.5" text-anchor="end">Insult</text>
<rect x="132" y="342" width="293.5" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="355" width="334.5" height="11" rx="4" fill="#3987e5"/>
<text x="474.5" y="364" fill="#e6e6ea" font-size="11.5" font-weight="600">0.93</text>
<text x="544" y="352" fill="#9a9aa4" font-size="11">+0.11</text>
<text x="122" y="388" fill="#e6e6ea" font-size="12.5" text-anchor="end">Self-harm</text>
<rect x="132" y="374" width="308.6" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="387" width="349.3" height="11" rx="4" fill="#3987e5"/>
<text x="489.3" y="396" fill="#e6e6ea" font-size="11.5" font-weight="600">0.97</text>
<text x="544" y="384" fill="#9a9aa4" font-size="11">+0.11</text>
<text x="122" y="420" fill="#e6e6ea" font-size="12.5" text-anchor="end">Toxicity</text>
<rect x="132" y="406" width="294.4" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="419" width="333.7" height="11" rx="4" fill="#3987e5"/>
<text x="473.7" y="428" fill="#e6e6ea" font-size="11.5" font-weight="600">0.93</text>
<text x="544" y="416" fill="#9a9aa4" font-size="11">+0.11</text>
<text x="122" y="452" fill="#e6e6ea" font-size="12.5" text-anchor="end">Scam/Incoherent</text>
<rect x="132" y="438" width="308.6" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="451" width="344.6" height="11" rx="4" fill="#3987e5"/>
<text x="484.6" y="460" fill="#e6e6ea" font-size="11.5" font-weight="600">0.96</text>
<text x="544" y="448" fill="#9a9aa4" font-size="11">+0.10</text>
<text x="122" y="484" fill="#e6e6ea" font-size="12.5" text-anchor="end">Profanity</text>
<rect x="132" y="470" width="325.3" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="483" width="347.2" height="11" rx="4" fill="#3987e5"/>
<text x="487.2" y="492" fill="#e6e6ea" font-size="11.5" font-weight="600">0.96</text>
<text x="544" y="480" fill="#9a9aa4" font-size="11">+0.06</text>
<text x="122" y="516" fill="#e6e6ea" font-size="12.5" text-anchor="end">Sexual (Explicit)</text>
<rect x="132" y="502" width="328.7" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="515" width="345.7" height="11" rx="4" fill="#3987e5"/>
<text x="485.7" y="524" fill="#e6e6ea" font-size="11.5" font-weight="600">0.96</text>
<text x="544" y="512" fill="#9a9aa4" font-size="11">+0.05</text>
<text x="122" y="548" fill="#e6e6ea" font-size="12.5" text-anchor="end">Sexual</text>
<rect x="132" y="534" width="328.9" height="11" rx="4" fill="#d95926"/>
<rect x="132" y="547" width="343.7" height="11" rx="4" fill="#3987e5"/>
<text x="483.7" y="556" fill="#e6e6ea" font-size="11.5" font-weight="600">0.95</text>
<text x="544" y="544" fill="#9a9aa4" font-size="11">+0.04</text>
</svg>

<figcaption style="margin-top:0.6rem;font-size:0.85rem;color:lch(61.683 1 272);">F1 score per label on our evaluation set, Supervisor 2.0 against 2.1, Arbiter model. Sorted by improvement.</figcaption>
</figure>

The same numbers as a table:

| Label | 2.0 | 2.1 | Change |
| --- | --- | --- | --- |
| Medical/Injury | 0.698 | 0.980 | +0.282 |
| Violence | 0.649 | 0.887 | +0.238 |
| Sexual (Unlawful) | 0.717 | 0.929 | +0.213 |
| Promotional | 0.752 | 0.946 | +0.194 |
| Sensitive | 0.761 | 0.950 | +0.190 |
| Hate/Racism | 0.765 | 0.954 | +0.189 |
| Spam | 0.772 | 0.959 | +0.188 |
| Harassment | 0.741 | 0.885 | +0.145 |
| Illegal | 0.765 | 0.897 | +0.132 |
| Insult | 0.815 | 0.929 | +0.114 |
| Self-harm | 0.857 | 0.970 | +0.113 |
| Toxicity | 0.818 | 0.927 | +0.109 |
| Scam/Incoherent | 0.857 | 0.957 | +0.100 |
| Profanity | 0.904 | 0.964 | +0.061 |
| Sexual (Explicit) | 0.913 | 0.960 | +0.047 |
| Sexual | 0.914 | 0.955 | +0.041 |

Violence and Medical/Injury were the two worst labels in 2.0, both under 0.70. They are now the two best.

## The false positive problem specifically

F1 rewards catching things, so it is not the number to look at if what you care about is the bot leaving innocent people alone. For that, the metric is how well the model recognises a message as safe.

Across the sixteen labels, that score went from 0.975 to 0.986. That sounds like a small move until you look at it as errors rather than successes: the rate of getting a harmless message wrong dropped from 2.5 percent to 1.4 percent.

<figure style="margin:1.75rem 0;">

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 560 150" width="100%" role="img" aria-label="Error rate on safe content, 2.0 versus 2.1" style="max-width:560px;height:auto;font-family:system-ui,-apple-system,Segoe UI,sans-serif">
<title>Error rate on harmless messages (lower is better)</title>
<text x="96" y="20" fill="#9a9aa4" font-size="12">Mistakes on harmless messages, lower is better</text>
<text x="86" y="59" fill="#e6e6ea" font-size="12.5" text-anchor="end">Supervisor 2.0</text>
<rect x="96" y="44" width="281.5" height="20" rx="4" fill="#d95926"/>
<text x="386.5" y="59" fill="#e6e6ea" font-size="12.5" font-weight="600">2.5%</text>
<text x="86" y="103" fill="#e6e6ea" font-size="12.5" text-anchor="end">Supervisor 2.1</text>
<rect x="96" y="88" width="157.5" height="20" rx="4" fill="#3987e5"/>
<text x="262.5" y="103" fill="#e6e6ea" font-size="12.5" font-weight="600">1.4%</text>
<line x1="96" y1="38" x2="96" y2="112" stroke="#262a33" stroke-width="1"/>
</svg>

<figcaption style="margin-top:0.6rem;font-size:0.85rem;color:lch(61.683 1 272);">Share of harmless messages the model gets wrong, averaged across all sixteen labels.</figcaption>
</figure>

**That is 44 percent fewer mistakes on safe content.**

That is a real improvement and it is the one the feedback was asking for. It is not a claim that false positives are solved. If Supervisor flags something it should not have, press 👎. That is exactly the signal that produced this release, and it is what will produce the next one.

## Short messages

The most common complaint we received was single words getting flagged. Messages like "join" or "wait" were being classified as spam, which is a bad look in any server where people talk normally.

This is a known weakness of models trained mostly on longer text: a very short message carries almost no context, and the model reaches for whatever weak signal it can find. 2.1 was trained with substantially more short-message data, and the Spam label specifically went from 0.772 to 0.959.

## The tiers

All three models were retrained. Observer and Sentinel now use smaller, faster base models than 2.0 did, which is what lets them stay cheap, so their numbers are not directly comparable to the Arbiter figures above. Average F1 on the evaluation set:

| Tier | Average F1 |
| --- | --- |
| Observer | 0.874 |
| Sentinel | 0.891 |
| Arbiter | 0.941 |

If you are on Observer or Sentinel and you moderate a busy server, Arbiter is where the accuracy is.

## Being straight about what this is

These numbers come from our own evaluation set, which we built and label ourselves. That is the right tool for tracking whether a retrain improved things, because it is the same yardstick across both versions. It is not an independent audit, and you should read any vendor quoting their own benchmark, including us, with that in mind.

What we can point at that is not self-scored is the feedback itself. The 👍 and 👎 votes are yours, they are recorded, and they are what we are steering by. That is a slower signal than a benchmark, and a more honest one.

## Rolling out

2.1 is live now for every tier, on every plan, at no extra cost. There is nothing to update. If Supervisor is already in your server, it is already running the new models.

Try it on something that used to get wrongly flagged in the [live demo](https://supervisor.gg/demo), or [add Supervisor to your server](https://invite.supervisor.gg).

And keep pressing the buttons.
