# j-p-courneya.github.io

Personal academic profile site for [Jean-Paul Courneya](https://j-p-courneya.github.io) — Bioinformationist at the Health Sciences & Human Services Library, University of Maryland, Baltimore.

Built with [Astro](https://astro.build) and deployed to GitHub Pages via GitHub Actions.

## Local development

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # build to dist/
```

## Updating content

All profile data (name, bio, links) is in [`src/pages/index.astro`](src/pages/index.astro) at the top of the file in the `profile` object.

To add a profile photo, drop a file named `avatar.jpg` into the `public/` folder and commit it.
