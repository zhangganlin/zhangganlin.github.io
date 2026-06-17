# Personal Website Redesign + Compaction — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Restyle the single-page Jekyll site (direction "Refined Classic": profile sidebar + card-based publications/projects, sans-serif, TUM-blue accent, fully responsive) while preserving all content, and delete template leftovers for a compact repo.

**Architecture:** The live site is one page — `_pages/about.md` (`permalink: /`) `include_relative`s `news.md`, `publications.md`, `projects.md`, `teaching.md`. The theme's `single` layout already renders an `author_profile` **sidebar**, so direction B needs mainly CSS polish there. New presentation lives in one compiled stylesheet (`_sass/_custom.scss`, already `@import`ed by `assets/css/main.scss`); inline `<style>` is removed from `about.md`. Each paper/project `<table>` becomes a `.pub-card`. The existing hover-video media block (`.one > video.two + img`, `data-prefix`) is moved **verbatim** into the card thumbnail to keep current behavior.

**Tech Stack:** Jekyll, kramdown, SCSS (Minimal Mistakes theme), Liquid, hand-written HTML fragments. No JS framework. No test suite — verification is a clean build + visual check in the README's Docker flow.

---

## Conventions for this plan

**No git commits until the very end.** The user requires the whole job finished before any `git add`/commit. Every task ends with a **Verify** step (build + visual), **not** a commit. Task 9 handles the single, user-gated commit.

**Verify command (Docker, from README).** Unless a task says otherwise, "serve & check" means run the site and open `http://localhost:4000`:

```bash
ml container/rootless-docker
export DOCKER_DATAROOT=/storage/local/zga/docker/dataroot
export DOCKER_TMPDIR=/storage/local/zga/docker/tmp
start_rootless_docker.sh --quiet
docker run --rm -it -p 4000:4000 -v ${PWD}:/src/site gh-pages \
  sh -c "BUNDLE_GEMFILE=/src/site/Gemfile bundle install && BUNDLE_GEMFILE=/src/site/Gemfile bundle exec jekyll serve -H 0.0.0.0 -P 4000"
```

Keep this running in one terminal across tasks; Jekyll rebuilds on file change. **Check every time at two widths:** desktop (≥768px) and mobile (<768px, use browser devtools device toolbar). A "clean build" means the `jekyll serve` output shows no `Liquid Warning`, no `Error`, and "done in N seconds".

---

## File Structure

- `_sass/_custom.scss` — **Modify.** Add all new styles (sidebar polish, section headings, institution logos, `.pub-card` system, pills, venue badge, responsive). This is the single home for presentation.
- `_pages/about.md` — **Modify.** Remove `<head>`/`<style>` blocks; keep bio (with 张甘霖 in intro), education logos, section includes; convert `## News` etc. to styled section headings.
- `_pages/publications.md` — **Modify.** Convert each `<table>` entry to `.pub-card`.
- `_pages/projects.md` — **Modify.** Same conversion.
- `_pages/news.md` — **Modify.** Wrap list with a class hook (keep collapse behavior).
- `_pages/teaching.md` — **Modify.** Wrap list with a class hook.
- `_layouts/single.html` — **Modify.** Remove includes for unused features (comments, social-share, breadcrumbs, toc, read-time, taxonomy, pagination, page__hero).
- **Deletes** (Tasks 7–8): `_source/`, `markdown_generator/`, `_drafts/`, `_data/comments/`, `CHANGELOG.md`, `Website.Rproj`, unreferenced layouts/includes, and unused `_config.yml`/`_config.dev.yml` blocks.

---

## Task 1: CSS foundation — design tokens, sidebar, section headings

**Files:**
- Modify: `_sass/_custom.scss` (append at end)

- [ ] **Step 1: Append design tokens, sidebar polish, section-heading, and institution-logo styles**

Append to `_sass/_custom.scss`:

```scss
/* ==========================================================================
   REDESIGN 2026 — Refined Classic
   ========================================================================== */

$accent: #0e396e;        // TUM blue
$accent-soft: #eef2f7;
$ink: #1f2733;
$muted: #6b7480;

/* Sidebar profile polish */
.author__avatar img {
  border-radius: 50%;
  border: 3px solid $accent-soft;
  max-width: 110px;
}
.author__name {
  font-weight: 700;
  letter-spacing: .2px;
}
.author__urls.social-icons li a:hover { color: $accent; }

/* Section headings (replaces bare h2/## headers) */
.section-heading {
  font-weight: 700;
  color: $accent;
  border-bottom: 2px solid $accent;
  display: inline-block;
  padding-bottom: 3px;
  margin: 1.6em 0 .8em;
  font-size: 1.35em;
}

/* Education / institution logo row */
.institution-list {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 14px;
  margin: 1em 0 1.5em;
}
.institution-list img {
  height: 34px;
  width: auto;
  padding: 4px 8px;
  border-radius: 4px;
  transition: transform .2s ease;
}
.institution-list a:hover img { transform: scale(1.08); }
```

- [ ] **Step 2: Verify**

Serve & check (command above). The page still renders (cards come later). Confirm: avatar is round with a soft border; the four education logos sit in a neat row and scale slightly on hover; build is clean at both widths.

---

## Task 2: Publication/project card CSS

**Files:**
- Modify: `_sass/_custom.scss` (append at end)

- [ ] **Step 1: Append the card system**

Append to `_sass/_custom.scss`:

```scss
/* Publication / project cards */
.pub-card {
  display: flex;
  gap: 18px;
  align-items: flex-start;
  border: 1px solid #ececec;
  border-radius: 10px;
  padding: 14px 16px;
  margin: 0 0 18px;
  background: #fff;
  transition: box-shadow .2s ease, transform .2s ease;
}
.pub-card:hover {
  box-shadow: 0 4px 16px rgba(14, 57, 110, .10);
}

.pub-thumb {
  position: relative;
  flex: 0 0 230px;
  max-width: 230px;
  border-radius: 6px;
  overflow: hidden;
  line-height: 0;
}
.pub-thumb img,
.pub-thumb video { width: 100%; border-radius: 6px; display: block; }

/* Venue badge in the thumbnail corner */
.pub-venue {
  position: absolute;
  top: 6px;
  left: 6px;
  z-index: 2;
  font-size: 11px;
  font-weight: 600;
  line-height: 1;
  color: #fff;
  background: $accent;
  padding: 4px 8px;
  border-radius: 4px;
  letter-spacing: .2px;
}

.pub-info { flex: 1 1 auto; min-width: 0; }
.pub-title {
  font-weight: 700;
  font-size: 1.05em;
  color: $ink;
  line-height: 1.3;
}
.pub-title a { color: $ink; }
.pub-title a:hover { color: $accent; }
.pub-authors { margin: 4px 0; font-size: .92em; }
.pub-venue-line { color: $muted; font-style: italic; font-size: .9em; }
.pub-abstract { margin: 8px 0 0; font-size: .9em; color: #444; }

/* Pill links */
.pub-links { margin: 8px 0 2px; display: flex; flex-wrap: wrap; gap: 6px; }
.pub-links a.pill {
  font-size: 12px;
  line-height: 1;
  padding: 5px 11px;
  border-radius: 14px;
  background: $accent-soft;
  color: $accent;
  font-weight: 600;
  text-decoration: none;
  transition: background .15s ease, color .15s ease;
}
.pub-links a.pill:hover { background: $accent; color: #fff; }
.pub-links a.pill--primary { background: $accent; color: #fff; }
.pub-links a.pill--primary:hover { background: darken($accent, 8%); }

/* Responsive: stack thumbnail above text on mobile */
@media (max-width: 768px) {
  .pub-card { flex-direction: column; gap: 12px; }
  .pub-thumb { flex-basis: auto; max-width: 100%; width: 100%; }
}
```

- [ ] **Step 2: Verify**

Serve & check. Nothing visually changes yet (no card markup exists), but the build must stay clean — confirm no SCSS compile error in the serve output (a bad `darken()`/variable would surface here).

---

## Task 3: Clean `about.md` — remove inline styles, keep content

**Files:**
- Modify: `_pages/about.md`

- [ ] **Step 1: Replace the whole file**

The current file has an inline `<head>` with `<style>` blocks (now in SCSS) and uses `## News`-style headings. Replace `_pages/about.md` with:

```markdown
---
permalink: /
title: "About me"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

<meta name="google-site-verification" content="xDNWUvx6Q5EWK5YYSyKvK8DZTmvXhKsGX203Ll-BFFE">

Hi, I'm Ganlin Zhang (张甘霖), a PhD student at <a href="https://www.tum.de/en/" target="_blank">Technical University of Munich</a>, supervised by <a href="https://cvg.cit.tum.de/members/cremers" target="_blank">Prof. Daniel Cremers</a>. Currently I focus on Visual SLAM, Structure from Motion and 3D reconstruction.

Previously, I received my Master's degree in Computer Science from <a href="https://ethz.ch/en.html" target="_blank">ETH Zurich</a>, where I worked on 3D Vision research projects with <a href="https://vision.ee.ethz.ch/people-details.OTAyMzM=.TGlzdC8zMjg3LC0xOTcxNDY1MTc4.html" target="_blank">Prof. Luc Van Gool</a> and <a href="https://people.inf.ethz.ch/marc.pollefeys/" target="_blank">Prof. Marc Pollefeys</a>. Before that, I obtained my Bachelor's degree in Computer Science from <a href="http://www.shanghaitech.edu.cn/eng/" target="_blank">ShanghaiTech University</a>, supervised by <a href="https://mpl.sist.shanghaitech.edu.cn/Director.html" target="_blank">Prof. Laurent Kneip</a>. During my undergraduate studies, I also spent a year at UC Berkeley, as a visiting student.

<div class="institution-list">
  <a href="https://www.tum.de/en/" target="_blank"><img src="./images/education/tum_logo_white.svg" style="background-color:#0e396e;"></a>
  <a href="https://www.ethz.ch/en" target="_blank"><img src="./images/education/eth_logo_white.svg" style="background-color:#215CAF;"></a>
  <a href="https://www.shanghaitech.edu.cn/eng/" target="_blank"><img src="./images/education/shanghaitech_logo.svg"></a>
  <a href="https://berkeley.edu" target="_blank"><img src="./images/education/ucb_logo.svg"></a>
</div>

<h2 class="section-heading">News</h2>
{% include_relative news.md %}

<h2 class="section-heading">Publications</h2>
{% include_relative publications.md %}

<h2 class="section-heading">Selected Projects</h2>
{% include_relative projects.md %}

<h2 class="section-heading">Teaching</h2>
{% include_relative teaching.md %}

<script type="text/javascript" id="clustrmaps" src="//cdn.clustrmaps.com/map_v2.js?cl=080808&w=400&t=tt&d=rM7BoV2_o5IxNyY7EAufsftBDgwOhxdU0h5gt6JOQ5o&co=ffffff&cmo=79c4d3&cmn=3a90cc&ct=80b2c6"></script>
```

Notes: 张甘霖 stays in the intro paragraph; the sidebar name comes from `_config.yml` `author.name: "Ganlin Zhang"` (already English-only — do **not** change it). The leading `---` horizontal rule and the inline `<style>`/`<head>` blocks are intentionally dropped.

- [ ] **Step 2: Verify**

Serve & check. Confirm: bio text intact incl. "(张甘霖)"; education logos render; four section headings show the blue underline style; the clustrmaps widget still loads; sidebar (left, desktop) shows avatar + "Ganlin Zhang" + social icons and collapses above content on mobile. Build clean.

---

## Task 4: Convert `publications.md` entries to cards

**Files:**
- Modify: `_pages/publications.md`

Each current entry is: a redundant `<heading><strong>Title</strong></heading>` line, then `<table class="responsive">` with a media `<td>` and a text `<td>`, then `<hr>`. Convert each to a `.pub-card`, **dropping the redundant `<heading>` line and the `<hr>`** (cards have their own spacing). **Move the media block — the entire `<div class="one">…</div>` including any `<video class="two shape">`, `<img>`, and the `data-prefix` attribute — verbatim** into `.pub-thumb`, adding only the `<span class="pub-venue">` badge. Convert the ` | `-separated links into `<a class="pill">` (make the first/primary link `pill--primary`).

- [ ] **Step 1: Worked example — replace the ViSTA-SLAM block**

Replace the ViSTA-SLAM entry (the `<heading>…ViSTA-SLAM…` line through its closing `</table>` and following `<hr>`) with:

```html
<div class="pub-card">
  <div class="pub-thumb" data-prefix="vista">
    <span class="pub-venue">3DV 2026</span>
    <div class="one">
      <div class="two shape" style="width: 100%;">
        <video autoplay muted loop playsinline width="100%">
          <source src="https://ganlinzhang.xyz/vista-slam/media/vista_slam.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video>
      </div>
      <img src="/images/publications/vista.png" style="width: 100%;" class="img"/>
    </div>
  </div>
  <div class="pub-info">
    <div class="pub-title"><a href="https://ganlinzhang.xyz/vista-slam" target="_blank">ViSTA-SLAM: Visual SLAM with Symmetric Two-view Association</a></div>
    <div class="pub-authors">
      <strong>Ganlin Zhang</strong>,
      <a href="https://shenhanqian.github.io/" target="_blank">Shenhan Qian</a>,
      <a href="https://xiwang1212.github.io/homepage/" target="_blank">Xi Wang</a>,
      <a href="https://cvg.cit.tum.de/members/cremers" target="_blank">Daniel Cremers</a>
    </div>
    <div class="pub-venue-line"><em><strong>3DV</strong> 2026</em></div>
    <div class="pub-links">
      <a class="pill pill--primary" href="https://ganlinzhang.xyz/vista-slam/" target="_blank">Project</a>
      <a class="pill" href="https://arxiv.org/abs/2509.01584" target="_blank">arXiv</a>
      <a class="pill" href="https://github.com/zhangganlin/vista-slam" target="_blank">Code</a>
    </div>
    <p class="pub-abstract">ViSTA-SLAM is a real-time monocular dense SLAM pipeline that combines a Symmetric Two-view Association (STA) frontend with Sim(3) pose graph optimization and loop closure, enabling accurate camera trajectories and high-quality 3D scene reconstruction from RGB inputs.</p>
  </div>
</div>
```

- [ ] **Step 2: Apply the same transform to the remaining entries**

Repeat exactly for every other entry. Keep each entry's media block, authors (own name bolded), abstract, and **all** links unchanged in content. Use this `pub-venue` badge text per entry (taken from each entry's `<em>` line). Order in the file stays as today:

1. **Flow4R** — badge `arXiv 2026`; no video (image only — put the `<img>` inside `.pub-thumb`, no `.two`); links: Project (primary), arXiv. Keep the existing `<em>Preprint on arXiv, 2026</em>` venue line and abstract.
2. **NOVA3R** — badge `ICLR 2026`; keep video; links: Project (primary), Paper, Code. Venue line `<em><strong>ICLR</strong> 2026</em>`.
3. **ViSTA-SLAM** — done in Step 1.
4. **SNI-SLAM++** — badge `TPAMI 2025`; keep video; links: Project (primary), Paper. Venue line `<em><strong>TPAMI</strong> 2025</em>`. Keep all 8 authors.
5. **Back on Track (BA-Track)** — badge `ICCV 2025`; keep video; links: Project (primary), arXiv, Code. **Preserve the orange "(Best Paper Candidate)" span** inside the venue line exactly: `<em><strong>ICCV</strong> 2025 <span style="color:rgb(255, 94, 0);font-weight: bold;">(Best Paper Candidate)</span></em>`.
6. **Splat-SLAM** — badge `CVPRW 2025`; image only; links: Paper (primary), Code. Keep the `*` co-author markers (`Erik Sandström*`, `Ganlin Zhang*`).
7. **GlORIE-SLAM** — badge `arXiv 2024`; keep video; links: Project (primary), arXiv, Code. Venue line `<em>Preprint on arXiv, 2024</em>`. Keep the two-line numbered abstract (use `<br>` as today).
8. **Revisiting Rotation Averaging** — badge `CVPR 2023`; image only; links: arXiv (primary), Code. Keep the two-line numbered abstract.

For image-only entries, `.pub-thumb` contains just `<div class="one"><img ... class="img"/></div>` (no `data-prefix`, no `.two`).

- [ ] **Step 3: Verify**

Serve & check. Confirm **all 8 publications present and in order**; each shows thumbnail + corner venue badge + title link + authors (your name bold) + italic venue line + pill links + abstract. Hover-video entries still play their video; image-only entries show the image. BA-Track still shows the orange "(Best Paper Candidate)". On mobile each card stacks (thumbnail full-width above text). Build clean (watch for Liquid warnings from stray `{`/`|` — there should be none since links are now plain HTML).

---

## Task 5: Convert `projects.md` entries to cards

**Files:**
- Modify: `_pages/projects.md`

`projects.md` uses the identical `<heading>` + `<table class="responsive">` + `<hr>` pattern. Apply the **same** transform as Task 4 (drop `<heading>`/`<hr>`, move media verbatim into `.pub-thumb`, pills for links, own name bold). Projects have **no formal venue**, so use the **course/workshop** as the badge text, kept short.

- [ ] **Step 1: Convert each project entry**

Badge text per project (from each `<em>` line; abbreviate to fit the corner badge), order unchanged:

1. **EgoSpot: Egocentric Multimodal Control for Hands-Free Mobile Manipulation** — badge `ICRA 2026 Workshop`; keep video; links: Project (primary), Code. Keep full `<em>Course project of Mixed Reality 2022 in ETH Zurich, accepted by ICRA 2026 MM-SpatialAI Workshop</em>` as the venue line.
2. **NICE-SLAM with Adaptive Feature Grids** — badge `ETH 3DV 2022`; keep video; links: Code. Keep full venue line and the description (including the NICE-SLAM link inside it).
3. **Optimization by Particle Swarm Using Surrogates…** — badge `ETH ASL 2022`; image only; links: Code. Keep the in-description paper link.
4. **Improved PSMNet for Deep Stereo Disparity Estimation** — badge `ETH DL 2021`; image only; links: Code.
5. **Robot Art: Using Robot Arm to Draw Pictures** (and any further entries below line 133) — badge from its `<em>` line; keep media verbatim; pills for any links.

If a project has multiple inline description links, keep them inside `<p class="pub-abstract">` as-is (only the top-level ` | ` action links become pills).

- [ ] **Step 2: Verify**

Serve & check. Confirm **every project present and in order**, each as a card with course/workshop badge, pill links, description intact (including in-text links), media preserved. Mobile stacks correctly. Build clean.

---

## Task 6: Restyle `news.md` and `teaching.md`

**Files:**
- Modify: `_pages/news.md`
- Modify: `_pages/teaching.md`

- [ ] **Step 1: Add a class hook to the news list (keep collapse behavior)**

In `_pages/news.md`, keep the existing `#news-container`/`#news-list` structure and every `<li>` item unchanged; only add `class="news-list"` to the `<ul>`:

```html
<div id="news-container" data-show="3" data-padding="0" style="overflow-y: auto; padding-right: 10px;">
  <ul id="news-list" class="news-list">
```

(Leave all `<li>` lines exactly as they are.)

- [ ] **Step 2: Append news/teaching list styling**

Append to `_sass/_custom.scss`:

```scss
/* News + teaching lists */
.news-list { list-style: none; margin: 0; padding: 0; }
.news-list li {
  padding: 6px 0;
  border-bottom: 1px solid #f0f0f0;
  font-size: .92em;
  line-height: 1.5;
}
.news-list li em { color: $accent; font-style: normal; font-weight: 600; margin-right: 6px; }

.teaching-list { padding-left: 1.1em; }
.teaching-list li { margin: 6px 0; line-height: 1.5; }
```

- [ ] **Step 3: Wrap the teaching list**

`teaching.md` is currently Markdown `*` bullets. Wrap them in a classed `<ul>` so the style applies. Replace `_pages/teaching.md` with:

```html
<ul class="teaching-list">
  <li>Practical Course: Deep Learning for Spatial AI: <a href="https://cvg.cit.tum.de/teaching/ss2026/dl4sai" target="_blank">2026 Summer</a>, <a href="https://cvg.cit.tum.de/teaching/ss2025/dl4sai" target="_blank">2025 Summer</a></li>
  <li>Master Seminar — Modern Methods for 3D Representation and Reconstruction: <a href="https://cvg.cit.tum.de/teaching/ws2025/seminar_mm3dr" target="_blank">2025/26 Winter</a></li>
  <li>Master Seminar — 3D Vision Foundation Models: <a href="https://cvg.cit.tum.de/teaching/ws2025/seminar_3dvfm" target="_blank">2025/26 Winter</a></li>
</ul>
```

- [ ] **Step 4: Verify**

Serve & check. News items show the date in blue with a thin divider between rows; the collapse/"show 3" behavior still works; teaching shows three styled bullets with working links. Build clean.

---

## Task 7: Slim `single.html`, delete unreferenced layouts/includes

**Files:**
- Modify: `_layouts/single.html`
- Delete: unreferenced layouts/includes (verified per step)

- [ ] **Step 1: Trace current usage (record the baseline)**

Run:

```bash
grep -rhoE "include(_relative)? +[a-zA-Z0-9_/.-]+" _layouts _includes _pages | awk '{print $2}' | sort -u
grep -rhoE "layout: *[a-z-]+" _pages _config.yml _layouts | sort -u
```

Expected rendered layouts: `single`, `archive` (sitemap.md), `default`, `compress`. Note this output to compare against after edits.

- [ ] **Step 2: Remove unused feature includes from `single.html`**

In `_layouts/single.html`, delete the include lines (and any now-empty wrapping markup around them) for features the site does not use: `breadcrumbs.html`, `page__hero.html`, `read-time.html`, `page__taxonomy.html`, `post_pagination.html`, `social-share.html`, `comments.html`, `toc.html`. **Keep** `sidebar.html`, `archive-single.html`, and `base_path`. Do not touch `default.html`'s includes (head/masthead/footer/scripts/browser-upgrade are all needed).

- [ ] **Step 3: Verify the page still renders before deleting anything**

Serve & check the homepage at both widths — sidebar, bio, all sections must still render. The page should look the same minus comment/share/toc/breadcrumb chrome (which was already off). Build clean.

- [ ] **Step 4: Delete layouts/includes now proven unreferenced**

Re-run the Step 1 greps. For each candidate below, delete **only if** it no longer appears in the include/layout reference output:

```bash
# layouts not reachable from rendered pages (about→single, sitemap→archive)
rm -f _layouts/splash.html _layouts/single-portfolio.html _layouts/archive-taxonomy.html _layouts/talk.html
# includes orphaned after Step 2 (confirm each is absent from the grep first)
rm -f _includes/page__hero.html _includes/page__taxonomy.html _includes/post_pagination.html \
      _includes/read-time.html _includes/social-share.html _includes/breadcrumbs.html _includes/toc.html
rm -rf _includes/toc
# template demo includes never referenced by the rendered set
rm -rf _includes/feature_row _includes/gallery
rm -f _includes/paginator.html _includes/archive-single-talk.html _includes/archive-single-talk-cv.html \
      _includes/archive-single-cv.html _includes/category-list.html _includes/tag-list.html \
      _includes/comment.html _includes/comments.html _includes/post_pagination.html
```

If a grep still shows a name, **keep that file** and note why. (`comments.html` is safe only after Step 2 removed its include from `single.html`.)

- [ ] **Step 5: Verify**

Serve & check both widths. **Critical:** the `jekyll serve` output must show **no** "Could not locate the included file" / "Liquid Exception". Homepage and `/sitemap/` and `/terms/` and `/404.html` must build. If any include error appears, restore the file it names. Build clean.

---

## Task 8: Delete template leftovers, clean config

**Files:**
- Delete: `_source/`, `markdown_generator/`, `_drafts/`, `_data/comments/`, `CHANGELOG.md`, `Website.Rproj`
- Modify: `_config.yml`, `_config.dev.yml`

- [ ] **Step 1: Delete unrelated template content**

```bash
rm -rf _source markdown_generator _drafts _data/comments
rm -f CHANGELOG.md Website.Rproj
```

- [ ] **Step 2: Remove unused config blocks from `_config.yml`**

Edit `_config.yml`:
- Delete the entire `collections:` block (publications/research/talks/projects — none exist on disk) and the matching per-collection entries under `defaults:` (the `_teaching`, `_publications`, `_research`, `_talks`, `_projects` scopes). Keep the `_posts` and `_pages` default scopes.
- Delete the `comments:` and `staticman:` blocks (no comment system is used).

Make these deletions surgically; do not alter unrelated keys (site title, author, plugins, SEO, sass).

- [ ] **Step 3: Remove the disqus block from `_config.dev.yml`**

Edit `_config.dev.yml` to drop the `comments:`/`disqus:` lines, leaving the `url`, `analytics`, and `sass` overrides.

- [ ] **Step 4: Verify**

Serve & check (a `_config.yml` change requires **restarting** `jekyll serve`). The whole site must build clean and look identical to end of Task 6. Confirm homepage, `/sitemap/`, `/terms/`, `/404.html` all render. Confirm at both widths.

---

## Task 9: Final verification + handoff (single commit, user-gated)

**Files:** none (verification + commit)

- [ ] **Step 1: Full content audit**

Serve & check. Tick every item: bio (with 张甘霖 in intro only), 4 education logos, News list + collapse, **all 8 publications** in order with correct badges/links/abstracts and BA-Track's orange tag, **all projects** in order, Teaching's 3 entries. Sidebar shows avatar + "Ganlin Zhang" (no Chinese) + social icons. Everything correct on desktop **and** mobile.

- [ ] **Step 2: Confirm no broken references / dead files remain**

```bash
grep -rIl "academicpages\|disqus\|staticman" _config.yml _config.dev.yml _layouts _includes || echo "clean"
ls _source markdown_generator _drafts _data/comments CHANGELOG.md Website.Rproj 2>&1 | grep -i "No such" && echo "deletes confirmed"
```

Expected: config/layout/include references to removed systems are gone; the listed paths no longer exist.

- [ ] **Step 3: Final clean build**

Restart `jekyll serve`; confirm output ends with "done in N seconds", zero warnings/errors.

- [ ] **Step 4: Show the user; commit only on approval**

Per the user's instruction, **do not commit until they confirm.** Present a summary of changes and the working preview. On explicit approval, commit everything in one go:

```bash
git add -A
git commit -m "$(cat <<'EOF'
Redesign homepage (Refined Classic) and compact repo

- Card-based publications/projects, profile sidebar, sans-serif, TUM-blue accent, responsive
- Move inline styles into _sass/_custom.scss
- Remove template leftovers (_source, markdown_generator, _drafts, demo comments, CHANGELOG, Website.Rproj)
- Slim single.html and delete unreferenced layouts/includes
- Drop unused collections/comments/staticman config

Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>
EOF
)"
```

---

## Self-Review (author check)

- **Spec coverage:** Layout B/sidebar → Tasks 1,3; sans-serif + TUM-blue + section headings → Tasks 1,3; card entries w/ badge + pills, content preserved → Tasks 2,4,5; 张甘霖 intro-only / sidebar English-only → Task 3; news/teaching/logos kept → Tasks 1,3,6; styles moved to `_sass` → Tasks 1–2; cleanup of leftovers + reference-traced layout/include pruning + config → Tasks 7,8; Docker testing at both widths → every Verify step; single deferred commit → Task 9. All spec sections mapped.
- **Placeholder scan:** Full CSS and a full worked card example are given; remaining entries are enumerated by name with exact badge text, links, and special cases (BA-Track orange tag, `*` co-authors, numbered abstracts) — no "TBD"/"similar to above" left abstract.
- **Type/name consistency:** Class names (`pub-card`, `pub-thumb`, `pub-venue`, `pub-info`, `pub-title`, `pub-authors`, `pub-venue-line`, `pub-links`, `pill`, `pill--primary`, `pub-abstract`, `section-heading`, `institution-list`, `news-list`, `teaching-list`) and SCSS vars (`$accent`, `$accent-soft`, `$ink`, `$muted`) are defined once (Tasks 1–2) and reused consistently. `darken($accent, …)` is valid SCSS.
- **Risk note:** Deletions in Tasks 7–8 are each gated on a grep showing no reference and an immediate build check, so a wrong guess surfaces instantly and is reversible (nothing is committed until Task 9).
