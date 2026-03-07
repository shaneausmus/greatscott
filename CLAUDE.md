# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal blog/portfolio for Shane Ausmus, built with Eleventy (11ty) and deployed via GitHub Actions to GitHub Pages at `https://shaneausmus.github.io/greatscott/`.

## Commands

```bash
npm start       # local dev server with live reload (http://localhost:8080)
npm run build   # production build → _site/
```

Install dependencies first: `npm install`

## Stack

- **Eleventy 3.x** — static site generator; config in `.eleventy.js`
- **Nunjucks** — templating language for layouts and pages
- **Markdown** — blog posts in `src/posts/`, converted automatically
- **`@11ty/eleventy-plugin-syntaxhighlight`** — server-side Prism.js code highlighting
- **KaTeX** — math rendering via CDN auto-render (opt-in per post with `math: true` in front matter)
- No CSS framework; plain CSS in `src/css/style.css`

## Structure

```
src/
├── _data/site.js           # global site metadata (title, url, year)
├── _includes/layouts/
│   ├── base.njk            # shell: nav, footer, KaTeX scripts
│   └── post.njk            # extends base.njk; wraps blog post content
├── css/style.css           # all styles; CSS custom properties at top
├── posts/                  # markdown blog posts
│   ├── posts.json          # sets layout + "posts" tag for all posts
│   └── *.md                # front matter: title, date, description, category, math
├── images/                 # static assets (passed through to _site/)
├── index.njk               # home page
├── about.njk               # about page
├── blog.njk                # blog listing page
├── projects.njk            # projects page
└── resume.njk              # written resume (no PDF embed)
```

## Adding a Blog Post

Create `src/posts/YYYY-MM-DD-slug.md` with this front matter:

```yaml
---
title: Post Title
date: 2025-01-15
description: One-sentence summary.
category: projects   # updates | projects | thoughts | recs
math: true           # omit if no LaTeX needed
---
```

- Code blocks: standard fenced ` ```language ` syntax — Prism handles highlighting server-side
- LaTeX: `$inline$` and `$$display$$` — only renders when `math: true` is set

## Design System

Colors (CSS custom properties in `style.css`):
- `--cobalt: #0047AB` — primary brand color
- `--cobalt-dark: #003380` — hover states
- `--cobalt-faint: #EBF2FF` — tag backgrounds, inline code backgrounds
- `--text: #111827`, `--text-muted: #6B7280`, `--border: #E5E7EB`

Font: Inter (Google Fonts). Monospace: JetBrains Mono / Fira Code (system fallback, not loaded).

## Deployment

Push to `master` → GitHub Actions builds with `npm run build` and deploys `_site/` to GitHub Pages.

**One-time setup required**: Go to repo Settings → Pages → change Source to **"GitHub Actions"** (not a branch).

The `pathPrefix: "/greatscott/"` in `.eleventy.js` ensures all asset and page URLs are correct for the project subdirectory. Use `{{ '/path' | url }}` in templates, not hardcoded absolute URLs.

## Resume Page

`src/resume.njk` contains placeholder content sourced from the 2020 Summer Update post and public profile info. Replace `<!-- TODO -->` sections with current experience after receiving LinkedIn content.
