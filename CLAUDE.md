# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-file static portfolio site. Everything — HTML, CSS, and JavaScript — lives in `index.html`. No build step, no framework, no package manager. Deployed to Netlify at [harshgolani.netlify.app](https://harshgolani.netlify.app).

To preview locally, open `index.html` directly in a browser or use any static server:
```
npx serve .
# or
python3 -m http.server
```

## Architecture

**All CSS is inline** in a `<style>` block near the top of `index.html`. It is compact but not minified — properties are grouped logically. Design tokens live in `:root` as CSS custom properties (`--bg`, `--accent`, `--text`, etc.).

**All JS is inline** at the bottom: two behaviors only — a scroll listener that adds `.scrolled` to the nav, and an `IntersectionObserver` that adds `.in` to `.reveal` elements for entrance animations.

**Typography system** uses three Google Fonts:
- `Playfair Display` — headings and display text
- `DM Mono` — labels, tags, monospace details
- `Outfit` — body and UI text

**Sections** in order: `hero` → `marquee` → `#projects` → `#about` → `#skills` → `#contact` → `footer`

## Key Patterns

**Scroll-reveal**: Add class `reveal` (and optionally `d1`/`d2`/`d3` for staggered delays) to any element — the IntersectionObserver handles the rest.

**Project cards** use `.proj-scan` (an absolutely-positioned `div` as a child) for the horizontal accent-line sweep on hover. Badge color variants: `.ba` (AI/ML, accent), `.bs` (SDE, muted), `.bd` (Data, teal), `.bp` (PM, violet).

**Responsive breakpoints**: `@media(max-width:900px)` collapses the project and skills grids to 1 column. `@media(max-width:640px)` hides the nav links and tightens spacing.

**Grid layouts** (projects, skills, about stats) use `gap:1px; background:var(--border)` on the grid container with `background:var(--bg1)` on cells — this renders 1px borders between cells without actual border properties.
