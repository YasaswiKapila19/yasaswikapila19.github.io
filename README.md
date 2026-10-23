# yasaswi.kapila — personal site

A small Hugo site with its own theme (no theme dependency), built on the "Yasaswi Kapila" design system: Bricolage Grotesque for headings, Newsreader for reading, JetBrains Mono for labels, one sunset red, amber lane dashes, and a dusk footer. Light and dark mode follow the visitor's system setting.

## Run it locally

1. Install Hugo extended 0.150 or newer (`brew install hugo`, `winget install Hugo.Hugo.Extended`, or `pip install hugo`).
2. From this folder: `hugo server`
3. Open http://localhost:1313

## Write a post

Create `content/posts/my-post.md`:

```markdown
---
title: "Post title"
date: 2026-10-20
description: "One sentence shown in the post list and under the title."
---

Your text in Markdown.
```

Add `draft: true` to keep a post out of the published site; `hugo server -D` still shows drafts.

## Edit the rest

- Home page intro and the "Off the clock" list: `content/_index.md`
- About page: `content/about.md`
- GitHub and LinkedIn links: uncomment them in `hugo.toml` and they appear in the footer
- Colours and type: the tokens at the top of `static/css/main.css`

## Publish on GitHub Pages

1. Create a public repo named `<your-username>.github.io` (or any name) and push this folder to `main`.
2. In the repo, go to Settings → Pages and set Source to "GitHub Actions".
3. The included workflow (`.github/workflows/pages.yml`) builds and deploys on every push.

Fonts are self-hosted under `static/fonts` (SIL Open Font License, via Fontsource).
