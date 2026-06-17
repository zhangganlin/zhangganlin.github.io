# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal academic website for Ganlin Zhang (PhD student, Computer Vision, TU Munich), served at https://ganlinzhang.xyz via GitHub Pages. It is a Jekyll site forked from the [academicpages](https://academicpages.github.io/) template, itself built on the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme. Most day-to-day edits are content (new papers/projects), not theme code.

## Running locally

```bash
bundle install                          # install ruby deps (delete Gemfile.lock if it errors)
bundle exec jekyll liveserve            # build + serve at localhost:4000, auto-rebuild on change
```

`_config.dev.yml` overrides `_config.yml` for local dev (sets `url: http://localhost:4000`, disables analytics). Jekyll does **not** auto-reload `_config.yml` changes — restart the server after editing it.

Docker alternative (see README.md for the full rootless-docker setup): runs `jekyll serve -H 0.0.0.0 -P 4000` against a `gh-pages` image with the repo mounted at `/src/site`.

There are no tests. The "build" is `jekyll build`; GitHub Pages runs it on push.

## Architecture — the key thing to understand

**This is effectively a single-page site, not a collection-driven one.** Although `_config.yml` declares `publications`, `research`, `talks`, and `projects` collections, the corresponding `_publications/` etc. directories do **not** exist and are unused. Ignore the collection config when adding content.

Instead, the homepage is `_pages/about.md` (`permalink: /`). Near its end it stitches the page together with `include_relative`:

```
{% include_relative news.md %}
{% include_relative publications.md %}
{% include_relative projects.md %}
{% include_relative teaching.md %}
```

So `_pages/news.md`, `publications.md`, `projects.md`, `teaching.md` are **section fragments of the front page**, not standalone routes. Navigation links (`_data/navigation.yml`) are in-page anchors like `/#publications`, `/#selected-projects`, `/#teaching`.

Each section file is **hand-written HTML** (responsive `<table>` layouts with custom tags like `<papertitle>`, `<heading>`, image columns, and per-paper links). To add a publication or project, copy an existing `<table>...</table>` block in the relevant fragment and edit it — there is no TSV/bib pipeline feeding the live site.

`markdown_generator/` (TSV → markdown scripts/notebooks from the upstream template) is legacy and not wired into the current single-page content. Don't reach for it when adding a paper.

## Where things live

- `_pages/` — the actual content (homepage + section fragments + `404.md`, `terms.md`, `sitemap.md`).
- `_data/navigation.yml` — top nav (anchor links into the homepage).
- `_data/authors.yml`, `_config.yml` (`author:` block) — profile/sidebar identity and social links.
- `images/` — `profile*.jpg`, plus `publications/`, `projects/`, `education/` asset folders referenced by the section HTML.
- `_includes/`, `_layouts/`, `_sass/` — inherited theme internals; touch only for layout/styling changes. Custom styles for this site go in `_sass/_custom.scss`; the homepage also has inline `<style>` blocks in `about.md`.
- `_site/`, `.sass-cache/` — generated output; never edit by hand (`_site/` is gitignored).

## Conventions

- Author name in publication/project listings is rendered as `<strong>Ganlin Zhang</strong>` to bold the site owner.
- Site URL is `ganlinzhang.xyz` (`CNAME`), distinct from the repo name `zhangganlin.github.io`.
- Match the existing hand-rolled HTML table structure and custom element names when editing sections — consistency across paper entries matters for the layout/CSS.
