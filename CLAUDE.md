# Supervisor blog

Markdown sources for supervisor.gg/blog. The website clones this repo at build
time and renders every post, so publishing is adding a file here.

## Writing rules

**No em dashes or en dashes. Ever.** Not `—`, not `–`. Use a comma, a colon,
parentheses, or two sentences. This applies to post bodies, frontmatter,
headings, and commit messages. Check before committing:

```bash
grep -n '—\|–' posts/*.md
```

- British spelling, sentence case for headings.
- Second person ("your server"), plain language, no hype.
- Contractions are fine. Exclamation marks are not.

## Accuracy

Everything published here is a public claim about a product people pay for, so
it has to survive being quoted back at us.

- **Verify before writing.** Numbers come from the repo, the database, an eval
  run, or a source you actually read in this session. Never from memory and
  never estimated.
- **Say where a number came from** if it is load bearing (eval set, model
  metadata, production telemetry), and say how big the sample was.
- **Do not publish an accuracy, precision, or false-positive rate that our own
  telemetry contradicts.** `moderation_feedback` in the production database is
  the ground truth for how the models are actually doing. If a marketing claim
  and that table disagree, the table wins and the claim does not ship.
- **Competitor claims get checked against their own docs**, not from memory. If
  the docs are unreachable, say what the source was and how confident it is, or
  leave the detail out. Do not assert specific limits, prices, or feature names
  you could not read.
- Prefer "we measured X on Y" to "X is the best". A concrete, checkable number
  is more persuasive than a superlative and cannot be disproven by a user.

## Tone for comparisons

Competitor posts (Carl-bot, Dyno) follow a fixed shape: say honestly what the
other tool is good at, explain where its approach runs out, explain what
Supervisor does differently, then land on "different tools, often run both".
Never imply a competitor is bad. Most readers already use one and will stop
reading if the post reads as an attack.

## Format

- `posts/<slug>.md`, filename is the URL slug.
- Frontmatter, quote any value containing a colon:

```yaml
---
title: "Post Title"
date: 2026-07-27
description: "One-line summary shown on the index and in meta tags."
---
```

- `date` is YYYY-MM-DD and drives the index sort, newest first.
- Body starts with `# Title` matching the frontmatter title.
- Standard markdown plus tables and fenced code blocks.
- Internal links are root relative: `/glossary/false-positive`, `/docs`,
  `https://supervisor.gg/demo`.
- Close with a call to action pointing at the live demo or the invite link.

## Do not

- Edit a published post to change history. A dated announcement stays as it was
  written; corrections go in a new post.
- Invent testimonials, customer names, or user counts.
- Claim a feature that is not shipped. "Coming soon" only if it genuinely is.
