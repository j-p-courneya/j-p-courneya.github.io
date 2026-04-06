# Site Maintenance Guide

Quick reference for keeping [j-p-courneya.github.io](https://j-p-courneya.github.io) up to date.

---

## Adding a Notes to File Post

1. Create a new `.md` file in `src/content/notes/`
2. The filename becomes the URL slug — e.g. `my-post.md` → `/notes/my-post`
3. Include this frontmatter at the top of the file:

```yaml
---
title: "Your Post Title"
date: YYYY-MM-DD
description: "One sentence summary — shown in the listing page."
draft: false
---
```

4. Write your content below the frontmatter in standard Markdown
5. To hide a post without deleting it, set `draft: true` — it won't appear in the listing or be accessible by URL

Posts are sorted by date, newest first.

---

## Adding a Code Along Tutorial Card

Edit the `codeAlongItems` array in `src/pages/index.astro` (starts around line 30):

```js
const codeAlongItems = [
  // Add a new entry like this:
  {
    title: 'Your Tutorial Title',
    type: 'Workshop',        // e.g. Workshop, Guide, Tutorial
    desc: 'One or two sentences describing what it covers.',
    href: 'https://github.com/j-p-courneya/your-repo',
  },
  // ...existing entries
];
```

Each card links directly to the resource — typically a GitHub repo. The `type` field appears as a small label on the card.

---

## Adding a Work Together Item

Edit the `workItems` array in `src/pages/index.astro` (starts around line 63):

```js
const workItems = [
  // Add a new entry like this:
  { title: 'Service Name', desc: 'Short description of what you offer.' },
  // ...existing entries
];
```

These are display-only cards (no links) — just a title and a sentence.

---

## Updating Profile Info

All profile data is in the `profile` object at the top of `src/pages/index.astro` (lines 5–20):

| Field | What it controls |
|---|---|
| `displayName` | Name shown in the hero and browser tab |
| `jobTitle` | Title line under your name |
| `institution` | First institution line (Center for Vaccine Development) |
| `university` | Second institution line (University of Maryland, Baltimore) |
| `email` | Contact email |
| `bio` | Paragraph text in the About section |
| `links` | Array of icon links (Email, GitHub, Scholar, ORCID, LinkedIn) |

To update a link, find its entry in the `links` array and change the `href` value.

---

## Local Development

```bash
npm install        # first time only — install dependencies
npm run dev        # start dev server at http://localhost:4321
npm run build      # production build to dist/
npm run preview    # preview the production build locally
```

The dev server hot-reloads on save, so you can see changes immediately without rebuilding.

---

## Deployment

Push to `master` — GitHub Actions (`.github/workflows/deploy.yml`) builds the site and deploys to GitHub Pages automatically.

No manual steps needed. Monitor progress under the **Actions** tab in the GitHub repo.

> **Tip:** Changes to `src/content/notes/` (new posts) and `src/pages/index.astro` (cards, profile) are the most common updates. Both deploy the same way — just commit and push to `master`.

---

## File Map

| Task | File |
|---|---|
| Add / edit a note | `src/content/notes/<slug>.md` |
| Add a Code Along card | `src/pages/index.astro` → `codeAlongItems` array |
| Add a Work Together card | `src/pages/index.astro` → `workItems` array |
| Update profile info or links | `src/pages/index.astro` → `profile` object |
| Change nav links | `src/components/Nav.astro` → `navLinks` array |
| Update styles | `src/styles/global.css` |
| Change the site URL | `astro.config.mjs` → `site` value |
| Notes schema (frontmatter fields) | `src/content/config.ts` |
