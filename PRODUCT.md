# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Professional network: peers, collaborators, and community contacts (e.g. from platform engineering, SRE, and infra communities) checking Rory's background or current work. Not primarily a recruiter-facing job-search site, though it can serve that purpose incidentally.

## Product Purpose

A personal site presenting Rory Caraher's engineering background, project work, and CV to people in his professional network. Success means an accurate, credible, low-friction reference point — someone can land here and quickly understand what he does and has done.

## Positioning

Platform/infrastructure depth: 12 years of experience concentrated in platform engineering, spanning cloud and bare metal, on-prem and off, full-stack and mobile. The site should read as a systems/reliability specialist's home base, not a generic full-stack portfolio.

## Operating Context

Hugo static site with a custom unpublished theme (`rorycaraher`), deployed to GitHub Pages via CI on push to `main`. The Projects page is data-driven: `content/projects/<slug>.md` stubs hold only a GitHub repo URL, and CI (`scripts/fetch-projects.sh`) resolves each project's name/description from the GitHub API into `data/projects.yaml` at build time. The Music page follows the same pattern: `content/music/<slug>.md` stubs hold a SoundCloud track URL and release date, and CI (`scripts/fetch-music.sh`) resolves each track's title/description from SoundCloud's public oembed endpoint into `data/music.yaml` at build time.

## Capabilities and Constraints

- Site is scoped to homepage (bio) + Projects (GitHub-linked cards) + CV (Work/Education lists) + Music (SoundCloud-linked track list). No blog or case-study section is planned — don't propose one.
- The Projects list is an explicitly curated set of repo URLs, not GitHub's pinned-items feature (see `docs/adr/0001-projects-sourced-from-explicit-repo-list.md`). Future work must not reintroduce auto-pinning.
- The Music list is likewise an explicitly curated set of SoundCloud track URLs, resolved via SoundCloud's public oembed endpoint rather than its official (subscription-gated) API (see `docs/adr/0002-music-sourced-from-explicit-track-list-not-official-api.md`). Future work must not reintroduce auto-enumerating "all public tracks" from the account.
- No testimonials, client quotes, user counts, or performance benchmarks exist. None should be fabricated in future design or content work.

## Brand Commitments

- Name: Rory Caraher.
- Secondary personal facet: musician — electronic music as NLTL (SoundCloud), drums in Berlin Jazz Workshop. Now has its own Music page (track list linking out to SoundCloud), referenced from the homepage bio, but placed last in the nav (after CV) and still treated as texture, not the site's primary positioning.

## Evidence on Hand

- CV work history (getolo, Y42, BrowserStack, Together Digital) and education (NUI Maynooth) in `content/cv/_index.md` — real, factual.
- Project repos linked from GitHub (`github.com/rorycaraher/*`); descriptions are resolved live from the GitHub API, not authored copy.
- Social links: GitHub, LinkedIn, SoundCloud (`hugo.toml` params).
- No testimonials, metrics, or press exist — do not invent any.

## Product Principles

1. Credibility over polish-for-its-own-sake: every claim traces to real history (CV, real repos) — nothing invented.
2. Platform/infra depth is the throughline; content and positioning should reinforce systems/reliability expertise, not dilute it into generic "full-stack developer" framing.
3. Minimal surface area by design: three sections (Home, Projects, CV) is a deliberate constraint, not a gap to fill with more pages.
4. The musician facet is texture, not the pitch — keep it present but secondary to the professional positioning.
