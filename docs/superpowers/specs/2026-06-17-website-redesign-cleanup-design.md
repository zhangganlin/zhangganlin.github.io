# Personal Website: Redesign + Compaction

**Date:** 2026-06-17
**Owner:** Ganlin Zhang
**Repo:** zhangganlin.github.io (served at ganlinzhang.xyz via GitHub Pages, Jekyll)

## Goals

1. **Compact the codebase** — delete template leftovers and dead code so the repo
   contains only what the live single-page site actually uses.
2. **Redesign for beauty** — modernize the layout and styling while preserving
   **all existing content**, fully responsive on desktop and mobile.

Non-goal: no new content, no blog, no change to hosting/deploy. No restructuring
of the single-page model (homepage `about.md` that `include_relative`s the
section fragments).

## Context (current state)

- The live site is effectively **one page**: `_pages/about.md` (`permalink: /`)
  includes `news.md`, `publications.md`, `projects.md`, `teaching.md` as inline
  HTML fragments.
- Styling currently lives in **inline `<style>` blocks inside `about.md`** plus
  the theme's `_sass`.
- Publications/projects are hand-written responsive `<table>` blocks (image left,
  text right) with custom tags (`<papertitle>`, `<heading>`).
- `_config.yml` declares `publications`/`research`/`talks`/`projects` collections
  that **do not exist on disk** and are unused.

## Design Decision (approved)

Direction **B — Refined Classic**, with these specifics:

- **Layout:** fixed left **profile sidebar** (photo, name, title, social icons) +
  main content column. On mobile (`< 768px`) the sidebar collapses to a
  **centered top header**; content stacks below.
- **Typography:** system **sans-serif** throughout (no serif).
- **Accent color:** TUM blue `#0e396e` (already used by the education logos).
- **Section headers** (News / Publications / Selected Projects / Teaching):
  sans-serif heading with an underlined accent rule.
- **Name:** sidebar shows **"Ganlin Zhang"** only. The Chinese name **张甘霖**
  appears **only in the intro paragraph**, not in the profile/sidebar.

### Publication & project entry (the repeating unit)

Each entry is a bordered card: **thumbnail with a venue badge in the top-left
corner** + title + authors (own name bolded) + venue line + **pill-button links**
(Project / PDF / Code / Video, etc.). On mobile the thumbnail goes full-width and
the card stacks. Every current entry is preserved 1:1 — only the wrapper markup
changes.

- **News:** keep the existing scrollable list, lightly restyled.
- **Teaching:** keep the list, lightly restyled.
- **Education logos:** keep the institution logo row in the intro/about area.

## Implementation Approach

### Styling

- Move all presentation out of inline `<style>` in `about.md` into a single
  compiled stylesheet (`_sass/_custom.scss`, already imported by `main.scss`).
- Keep the small responsive rules but consolidate them there.
- Re-template the section fragments (`publications.md`, `projects.md`,
  `news.md`, `teaching.md`) to the new card structure, reusing a consistent
  class-based markup so all entries share one CSS definition.

### Cleanup — delete (verified unrelated to the live site)

- `_source/` (template author's R-Markdown blog posts)
- `markdown_generator/` (unused TSV→markdown pipeline)
- `_drafts/` (empty)
- `_data/comments/` (template demo comments)
- `CHANGELOG.md`, `Website.Rproj` (upstream template artifacts)
- `_config.dev.yml` disqus block; unused `collections`, `comments`, `staticman`
  config in `_config.yml`.

### Cleanup — dead layouts/includes (reference-traced, not blind)

The only rendered layouts are **`single`** (about, news, projects, publications,
teaching, terms, 404) and **`archive`** (sitemap.md). Their include tree was
traced.

- **Safe to delete now** (not reachable from any rendered page): layouts
  `splash.html`, `single-portfolio.html`, `archive-taxonomy.html`, `talk.html`;
  includes not in the rendered tree (e.g. `feature_row/`, `gallery/`,
  `paginator.html`, `archive-single-talk*.html`, `archive-single-cv.html`,
  `category-list.html`, `tag-list.html`, `page__taxonomy.html`,
  `post_pagination.html` — each confirmed unreferenced before removal).
- **Caveat:** `single.html` currently `include`s `comments.html`,
  `social-share.html`, `breadcrumbs.html`, `page__hero.html`, `read-time.html`,
  `archive-single.html`, `toc.html`. These are reachable, so for max compactness
  we will **first slim `single.html`** to drop features the site doesn't use
  (comments, social-share, breadcrumbs, toc, read-time, taxonomy, pagination),
  **then** delete the includes that become unreferenced. Each removal is gated on
  a repo-wide grep showing no remaining reference.

**Rule:** nothing is deleted until a grep confirms it is unreferenced from the
rendered set. If in doubt, keep it.

### Keep

The 4 section fragments, `about.md`, `sitemap.md`/`terms.md`/`404.md`, the
rendered layouts/includes (slimmed), `assets/`, `images/`, `CNAME`, SEO files
(`googleda9d52b32005d25d.html`, robots/sitemap plugins), `Gemfile`, analytics.

## Testing

Per the README's Docker flow: rebuild with `jekyll serve` (rootless-docker image,
port 4000) and visually verify after each meaningful change. Check **both**
desktop (≥768px) and mobile (<768px) widths. Confirm every pre-existing
publication, project, news item, teaching entry, link, and image still renders
before considering a step done.

## Acceptance Criteria

- All prior content present and correct (papers, projects, news, teaching, links,
  images, education logos, bio incl. 张甘霖 in intro only).
- New sidebar + card layout renders correctly on desktop and mobile.
- Styling lives in `_sass`, not inline in `about.md`.
- Deleted items confirmed unreferenced; site builds clean in Docker with no
  broken layouts/includes.
- Repo no longer contains the listed template leftovers.
