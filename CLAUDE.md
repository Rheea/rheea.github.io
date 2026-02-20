# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

This is a Jekyll-based personal portfolio website. Key commands:

- **Local development**: `bundle exec jekyll serve` (serves at http://localhost:4000)
- **Install dependencies**: `bundle install`
- **Build site**: `bundle exec jekyll build`

## Architecture Overview

Jekyll 3.7.4 static site for an academic/research portfolio, deployed via GitHub Pages.

### Data-Driven Content Model

The site is primarily content-driven through YAML data files rather than markdown pages:

- `_data/settings.yml` - Central content hub: menu items, bio (HTML with `| markdownify`), contact info, social links, Google Analytics config. Blog, about page, and projects sections are present but commented out.
- `_data/layout.yml` - Theme configuration: accent color (`#c99065`), text/background colors, animation preset.
- `_data/publications/publications.yml` - Main publications list with sections: Patents, Journals, Conferences, Invited Talks, PhD Thesis. Content is raw HTML/markdown rendered via `| markdownify` in `pages/research.html`.
- `_data/publications/<name>.yml` - Individual publication detail pages with embedded YouTube videos, slides, PDF/BibTeX download links.

### Dynamic SASS Theming

`assets/css/all.sass` uses **Liquid templating inside SASS** to inject color/animation variables from `_data/layout.yml`. Theme changes are made in the YAML file, not in CSS. The SASS follows a 3-tier SMACSS structure: `1-tools/` (bourbon, animations, fonts), `2-base/` (typography), `3-sections/` (component styles).

### Publications System

Publications are the core feature. Each publication can have:
- PDF in `publications/`
- BibTeX citation in `publications/bibtex/`
- Poster in `publications/posters/`
- Redirect HTML page in `publications/` (e.g., `gait17ral.html`)
- Detail YAML in `_data/publications/` with multimedia embeds

The publications list in `publications.yml` is authored as HTML within the YAML `papers` field and rendered with `| markdownify`.

### Layouts & Templates

Three layouts (`_layouts/`): `default.html` (master, includes MathJax + jQuery 2.1.1 + Font Awesome 4.7.0 from CDN), `page.html`, `post.html` (with optional Disqus). Partials in `_includes/`: header, footer, analytics, disqus, thumbnails.

### Deployment

GitHub Pages auto-deploys on push. No CI/CD pipeline. Output goes to `_site/` (gitignored).