# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based GitHub Pages personal academic profile site for J-P Courneya (Bioinformationist, University of Maryland HS/HSL). The site compiles and deploys automatically when commits are pushed to the repository — there is no local build step required.

Live site: `https://j-p-courneya.github.io`

## Development

There are no local build scripts. To preview locally with Jekyll installed:

```bash
jekyll serve
# or
bundle exec jekyll serve
```

The built site outputs to `_site/` (gitignored).

## Architecture

The site is intentionally minimal:

- **`_config.yml`** — All profile data (`name`, `email`, `job_title`, `institution`, `github_username`). Liquid variables like `{{ site.name }}` in templates pull from here.
- **`index.html`** — Single-page site. Uses YAML front matter (empty `---` delimiters) to trigger Jekyll processing. Inlines critical CSS and uses Basscss v7.1.1 (CDN) for utility classes.
- **`css/index.css`** — Custom styles extending Basscss, including responsive typography and flex utilities.

## Deployment

Push to the `main` branch. GitHub Pages automatically runs Jekyll and publishes the site. No CI configuration needed.
