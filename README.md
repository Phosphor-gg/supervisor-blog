# Supervisor blog

Markdown sources for [supervisor.gg/blog](https://supervisor.gg/blog).

The website builds the blog from this repo: a pre-build step clones it,
renders every post to HTML, and generates the date-sorted index, so
publishing is adding a markdown file here and rebuilding the website.

## Conventions

- Posts live in `posts/<slug>.md`; the filename is the URL slug
  (`posts/hello-world.md` becomes `/blog/hello-world`).
- Every post starts with frontmatter:

```yaml
---
title: Post Title
description: One-line summary shown on the index and in meta tags.
date: 2026-07-05
---
```

- `date` (YYYY-MM-DD) is the publish date; the index sorts by it, newest
  first.
- Quote any frontmatter value containing a colon.
- Standard markdown plus tables and fenced code blocks. Start the body
  with a `# Title` heading.
