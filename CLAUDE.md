# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Astro-based GitHub Pages personal academic profile site for Jean-Paul Courneya — Lead Bioinformatics Analyst at the Center for Vaccine Development, University of Maryland, Baltimore.

Live site: `https://j-p-courneya.github.io`

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Local dev server at localhost:4321
npm run build     # Build to dist/
npm run preview   # Preview the production build locally
```

## Deployment

Push to `master` — GitHub Actions (`.github/workflows/deploy.yml`) builds with `npm run build` and deploys `dist/` to GitHub Pages automatically. Source must be set to **GitHub Actions** in repo Settings → Pages.

## Architecture

Single-page site — all content lives in two files:

- **`src/pages/index.astro`** — The entire page. Profile data (name, email, title, institution, bio, links) is in the `profile` object at the top of the frontmatter. Edit here to change any content. Avatar pulls from `https://avatars.githubusercontent.com/u/11720131` (GitHub profile photo).
- **`src/styles/global.css`** — All styles. CSS radial-gradient deep-space background, animated canvas starfield (inline `<script>` in index.astro), `clamp()` for responsive typography. No CSS frameworks.
- **`astro.config.mjs`** — Sets `site` for the production URL.
- **`public/`** — Static assets. Empty currently; a local `avatar.jpg` here would take precedence if the img src is updated to point to it.
