# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Hugo static site (rorycaraher.com) using a custom, unpublished theme (`rorycaraher`) that lives at `themes/rorycaraher/` directly in this repo — despite the empty `.gitmodules` file, it is a regular tracked directory, not a git submodule.

## Commands

- `hugo server -D` — run the local dev server with drafts (http://localhost:1313/)
- `hugo --minify` — production build, outputs to `public/` (gitignored)
- `hugo new posts/<slug>.md` — scaffold a new blog post using `archetypes/posts.md`
- No test suite, linter, or package.json — there is no JS/CSS build tooling beyond Hugo's own asset pipeline (`resources.Get` + `minify`/`fingerprint`/`js.Build` in the theme's `head/css.html` and `head/js.html` partials).
- CI (`.github/workflows/deploy-website.yml`) pins `hugo-version: 0.153.3` (extended) and deploys `public/` to GitHub Pages on push to `main`. The locally installed Hugo may be a newer version — if a template feature behaves unexpectedly, check compatibility against 0.153.3.

## Architecture

- **Content** (`content/`) lives in TOML front matter (`+++` delimited), not YAML/JSON. Sections: `_index.md` (home, freeform markdown body — no front matter params beyond title/date/draft), `cv/_index.md` (Work + Education history as flat bullet lists under `##` headings, rendered as `.Content` inside a single markdown page — not individual pages per job), `projects/_index.md` + `projects/<slug>.md` (see below).
- **Projects** are a headless content type: each `content/projects/<slug>.md` holds only a `repo` front-matter param (the GitHub URL) plus `[build]` `render = "never"` / `list = "always"`, so it never gets its own routable page — it exists purely as data for `themes/rorycaraher/layouts/projects/list.html` to range over. That template joins each stub's `repo` URL against `site.Data.projects` (a `data/projects.yaml` map keyed by URL, holding `name`/`description`) to render one card per project, with the whole card wrapped in a link that opens the repo in a new tab.
- `data/projects.yaml` is generated in CI by `scripts/fetch-projects.sh`, which reads the `repo` URLs out of `content/projects/*.md` and resolves each one's name/description via the GitHub REST API (`GET /repos/{owner}/{repo}`) — not GitHub's pinned-items feature (see `docs/adr/0001-projects-sourced-from-explicit-repo-list.md`). The file carries a "do not edit manually" header and is empty in git until CI (or a local run with `GITHUB_TOKEN` set) populates it. To list a new project, add a `content/projects/<slug>.md` stub with its `repo` URL — don't edit `data/projects.yaml` directly.
- **Music** follows the identical headless pattern one level down: each `content/music/<slug>.md` holds a `track` param (the SoundCloud track URL — named `track`, not `url`, because Hugo reserves the `url` front-matter key for overriding a page's own permalink) plus a `date` param (the track's release date, used to sort newest-first) and the same `render = "never"` / `list = "always"` build block. `themes/rorycaraher/layouts/music/list.html` joins each stub's `track` against `site.Data.music` (a `data/music.yaml` map keyed by URL, holding `title`/`description`) to render one text-only row per track — no artwork, no embedded player — linking out to SoundCloud in a new tab.
- `data/music.yaml` is generated in CI by `scripts/fetch-music.sh`, which reads the `track` values out of `content/music/*.md` and resolves each one's title/description via SoundCloud's public, keyless `oembed` endpoint — not SoundCloud's official (subscription-gated) API (see `docs/adr/0002-music-sourced-from-explicit-track-list-not-official-api.md`). Same "do not edit manually" / empty-until-CI convention as `data/projects.yaml`. To list a new track, add a `content/music/<slug>.md` stub with its `track` URL and `date` — don't edit `data/music.yaml` directly.
- **Layouts** follow standard Hugo lookup order under `themes/rorycaraher/layouts/`: `_default/baseof.html` is the shared shell (header/main/footer), with `_default/home.html`, `_default/list.html`, `_default/single.html`, and a section-specific `projects/list.html` overriding `main`. `data-theme="dark"` is hardcoded on the `<html>` tag in `baseof.html`.
- **Nav menu** (`partials/menu.html`) is a generic recursive walker driven entirely by `[[menus.main]]` entries in `hugo.toml` — don't hardcode nav links in templates, add/edit menu entries in `hugo.toml` instead. Active-page highlighting relies on `class="active"` being on the `<li>` (not the `<a>`), paired with CSS in `mgplus.css` targeting `.mg-nav ul > li.active`.
- **CSS**: `themes/rorycaraher/assets/css/mgplus.css` holds the design system (CSS custom properties for colors, the `mg-*` grid/utility classes like `mg-row`/`mg-x12`/`mg-container`, card/tag styles). `main.css` is currently empty and reserved for page-specific overrides. Both are processed through Hugo Pipes (minify + fingerprint in production, raw `<link>` in `development` env) via `partials/head/css.html`.
- **JS**: `themes/rorycaraher/assets/js/main.js` is built via `js.Build`/esbuild through `partials/head/js.html`; currently near-empty.

## Working with `docs/agents/`

This repo has Claude Code agent-skill config docs:
- `docs/agents/domain.md` — describes a `CONTEXT.md`/`docs/adr/` domain-modeling convention. Both now exist at the repo root: `CONTEXT.md` defines the "Project" and "CV" terms, `docs/adr/` holds one ADR (`0001-projects-sourced-from-explicit-repo-list.md`) on why Projects data comes from an explicit repo list rather than GitHub's pinned items.

## Stale planning files

`PRD.md` and `progress.txt` document an even earlier redesign (dark theme, dedicated `/projects/` and `/music/` pages, a `soundcloud` shortcode) than the one currently in place. The site briefly consolidated Projects and Music into a single `/extras/` section, then split again: as of this writing there's a dedicated `/projects/` page (GitHub-linking cards only, no music) and Music was folded into the homepage's freeform body instead of getting its own page. Don't treat `PRD.md`/`progress.txt` as a description of current architecture; the Architecture section above reflects what's actually in place.
