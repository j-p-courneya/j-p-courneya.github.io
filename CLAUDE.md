# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Astro-based GitHub Pages personal academic profile site for J-P Courneya (Bioinformationist, University of Maryland HS/HSL).

Live site: `https://j-p-courneya.github.io`

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Local dev server at localhost:4321
npm run build     # Build to dist/
npm run preview   # Preview the production build locally
```

## Deployment

Push to `master` — GitHub Actions (`.github/workflows/deploy.yml`) builds with `npm run build` and deploys `dist/` to GitHub Pages automatically.

**One-time setup required:** In GitHub repo Settings → Pages, set the source to **GitHub Actions** (not "Deploy from a branch").

## Architecture

The site is intentionally minimal — a single landing page:

- **`src/pages/index.astro`** — The entire site. Profile data (name, email, job title, institution, GitHub username) is defined as a `profile` object in the frontmatter at the top of this file. Update it here to change any personal details.
- **`src/styles/global.css`** — All styles. Uses a CSS radial-gradient deep-space background, `clamp()` for responsive typography, and CSS custom properties. No external CSS frameworks.
- **`astro.config.mjs`** — Minimal Astro config; sets `site` for the production URL.
- **`public/`** — Static assets served at the root. Drop a `bg.jpg` here to replace the CSS gradient with a photo background (then update `global.css` to reference it).
