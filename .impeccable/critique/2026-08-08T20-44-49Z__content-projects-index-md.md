---
target: projects
total_score: 20
max_score: 32
na_heuristics: 7,10
p0_count: 1
p1_count: 1
timestamp: 2026-08-08T20-44-49Z
slug: content-projects-index-md
---
Method: dual-agent (A: general-purpose design-review · B: general-purpose detector/browser-evidence)

## Design Health Score

| # | Heuristic | Score | Key Issue |
|---|-----------|-------|-----------|
| 1 | Visibility of System Status | 2/4 | Nav active-state (violet text + underline, per DESIGN.md) never fires on any page — confirmed live, no `class="active"` or `aria-current` anywhere in rendered HTML |
| 2 | Match System / Real World | 3/4 | Plain, recognizable "card links to repo" pattern; descriptions are terse but legible |
| 3 | User Control and Freedom | 3/4 | External links open in new tabs (preserves place) but with no visual cue that they will |
| 4 | Consistency and Standards | 2/4 | Broken active-nav state contradicts DESIGN.md's own spec; two identically-styled giant violet headings compete at the top of the page |
| 5 | Error Prevention | 2/4 | No input surface to err on; the one real failure mode (empty state if CI fails) has no recovery path |
| 6 | Recognition Rather Than Recall | 3/4 | Nav labels are clear; "where am I" relies on recall since active-state is broken |
| 7 | Flexibility and Efficiency | n/a | Informational link-out surface; no power-user path applies |
| 8 | Aesthetic and Minimalist Design | 3/4 | Strong restraint (flat, single-accent, hairline borders) undercut by raw GitHub slugs as titles and an orphaned 4th grid item |
| 9 | Error Recovery | 2/4 | Empty state (`.card-empty`) is one unstyled grey line with zero next step |
| 10 | Help and Documentation | n/a | Not needed for a simple link-out grid |
| **Total** | | **20/32** | **Acceptable (63%)** |

## Design Specificity Verdict

**LLM assessment**: The *visual system* is confidently authored for this product — flat charcoal/graphite/violet, weight-300 type throughout, hairline 4px-radius cards, violet reserved strictly for interactive state. It reads as "engineering logbook," not a generic template. But the *content* on this specific page undercuts that specificity: all four cards show raw, unedited GitHub API description strings and raw kebab-case slugs as titles ("nltl-video-gen," "difference-engine"). Nothing on the page signals the stated positioning — "platform/infrastructure depth, systems/reliability specialist" (PRODUCT.md) — no stack tag, no framing of why a project matters to a peer infra engineer. The container is bespoke; the payload is generic.

**Deterministic scan**: `detect.mjs --json` ran clean (exit 0, `[]`) across `content/projects`, `themes/rorycaraher/layouts/projects`, `themes/rorycaraher/layouts/_default/baseof.html`, and `themes/rorycaraher/layouts/partials` — zero rule violations. The live-rendered URL scan (`detect.mjs --json http://localhost:1313/projects/`) could not run — `puppeteer is required for URL scanning` and it isn't installed, so this was a tool-unavailability result, not a real "clean" verdict for the rendered page. No false positives to reconcile (nothing fired).

**Visual overlays**: Not available this run — no `mcp__claude-in-chrome__*` browser-automation tooling was exposed in either sub-agent's session, so the mutation-preflight/`live-server.mjs`/console-overlay flow could not execute. Evidence instead came from direct `curl` of the rendered dev-server HTML (confirmed in the parent context too) plus full source/CSS reading. No user-visible in-browser overlay exists for this run.

## Overall Impression

The design system itself is disciplined and genuinely on-brand — restrained, monochrome, single-accent, no shadows, weight-300 throughout. What's actually broken is two levels below the visual system: a real functional bug (the nav's active-state has never fired on any page of the live site) and a content gap (the four project descriptions read as generic hobby-project blurbs with zero connection to the stated "systems/reliability" positioning). The biggest opportunity is closing that content gap — right now the page's craft signals credibility that its copy doesn't back up.

## What's Working

1. **Faithful, restrained execution of the design system** (`mgplus.css:142-156`): hairline `0.1rem solid var(--color-border)` card borders, `0.4rem` radius, violet appearing only on `:hover`/`:focus-visible` border-color and nowhere else — a genuinely disciplined implementation of "accent never decorative."
2. **Whole-card-as-link is accessible, not an anti-pattern** — `list.html:11` wraps a real `<h3>` + `<p>` inside a real `<a>`, giving screen readers a coherent accessible name ("difference-engine, Creates a unique version…") instead of an ambiguous clickable div.
3. **Responsive collapse is clean** — `mg-x12`/`mg-m4` drop the grid to full-width single column below 769px with generous `2rem 2.4rem` card padding, avoiding the most common mobile-grid failure (squished columns).

## Priority Issues

**[P0] Nav active-state has never worked on any page of the live site.** Curled `/`, `/projects/`, and `/cv/` directly (confirmed independently in the parent context too) — no `<li>` ever receives `class="active"`, and `aria-current="page"` never appears anywhere.
- **Why it matters**: DESIGN.md explicitly specifies violet text + violet underline for the active nav item — a stated, load-bearing feature that has silently never functioned. It's both a Nielsen #1 (visibility of system status) failure and a real accessibility gap (screen-reader users get no programmatic "current page" signal anywhere on the site).
- **Root cause (confirmed)**: `hugo.toml:13-26` defines all three `[[menus.main]]` entries with a plain `url` string. Hugo's `IsMenuCurrent`/`HasMenuCurrent` (used in `themes/rorycaraher/layouts/partials/menu.html:26-31`) only resolve a menu entry to a `Page` — and thus can match the current page — when the entry is defined via `pageRef` (or in page front matter). A `url`-only entry never resolves, so the check silently always returns false.
- **Fix**: change the three menu entries in `hugo.toml` to use `pageRef = '/'`, `pageRef = '/projects/'`, `pageRef = '/cv/'` instead of `url`, then re-verify `class="active"` / `aria-current="page"` render on each page.
- **Suggested command**: `/impeccable harden` (or a direct fix — this is a one-line-per-entry config change, not a design-judgment call)

**[P1] Card content doesn't carry the site's stated positioning.** Descriptions are unedited GitHub API pulls (`data/projects.yaml`, generated by `scripts/fetch-projects.sh`) — all four read as audio/video generative-art tooling or a notes app, with nothing signaling "platform/infrastructure depth, systems/reliability specialist" (PRODUCT.md's stated positioning).
- **Why it matters**: For the target audience (peers/collaborators evaluating Rory's engineering background), the page's disciplined visual credibility isn't backed by content that demonstrates the claimed expertise — a peer gets curiosity without payoff before being sent off-site to GitHub.
- **Fix**: hand-author a short blurb per project (small edit to the data step or an override field per stub) framed around the systems/infra angle, or surface GitHub's `language`/topic data as a lightweight tag per card so the grid actively signals the intended positioning instead of reading as a generic side-project list.
- **Suggested command**: `/impeccable clarify`

**[P2] Orphaned grid row at the current project count.** 4 cards in a 3-up grid (`.mg-m4` = 33.33%, `mgplus.css:96`) leaves row 2 with 1 card and two column-widths of dead space at ≥769px.
- **Why it matters**: breaks the compositional intentionality the rest of the system works hard to project — a visibly unbalanced grid on a page meant to demonstrate craft.
- **Fix**: move to a 2-up breakpoint (balances evenly at 2/4/6/8 projects) or explicitly design the grid to tolerate growth past today's 4-project count.
- **Suggested command**: `/impeccable layout`

**[P2] Empty state is a bare, structurally inconsistent failure surface.** `list.html:18-20` + `.card-empty` (`mgplus.css:173-175`) render a single line of muted grey text with no border, no card frame, and no recovery link — a real, CI-dependent possibility since `data/projects.yaml` stays empty until `scripts/fetch-projects.sh` runs successfully.
- **Why it matters**: on the page most responsible for demonstrating credibility, a bare "No projects to show right now." with zero next step reads as a bug, not a designed state, if CI ever fails silently.
- **Fix**: wrap the empty message in the same hairline-border card treatment used elsewhere, and add an inline link to the GitHub profile as a fallback.
- **Suggested command**: `/impeccable harden`

**[P3] Heading hierarchy skips h2, and raw kebab-case slugs are used verbatim as card titles** (`list.html:12` renders `.name` — e.g. "nltl-video-gen" — directly as `<h3>`, with no `<h2>` anywhere on the page).
- **Why it matters**: minor, but compounds the "generic auto-generated grid" feel and complicates screen-reader heading navigation (jumping by level lands on `h3` with no `h2` context).
- **Fix**: humanize project names for display (e.g. "NLTL Video Gen") while keeping the repo link/slug as the href, and insert a genuine `h2` section label if one is warranted.
- **Suggested command**: `/impeccable clarify`

## Persona Red Flags

**Jordan (First-Timer — a peer or contact arriving cold)**: No visual cue that clicking a card opens a new tab (`target="_blank"` with no icon or label) — may read as "did my click register?" Raw slug names like "nltl-video-gen" give an unfamiliar visitor no immediate sense of what the project is beyond the terse description.

**Sam (Accessibility-Dependent)**: The nav active-state bug is most acute here — `aria-current="page"` never fires anywhere on the site (confirmed live), so a screen-reader user gets zero programmatic "current location" signal on any page. Heading hierarchy skips `h2` (`menu.html` nav has no landmark labeling issue, but `list.html`'s `h1`→`h3` jump does), complicating heading-based navigation. New-tab links carry no `aria-label` suffix or visually-hidden "(opens in new tab)" text.

**Casey (Mobile)**: Card grid itself degrades cleanly per CSS (`mg-x12` full-width below 769px, generous `2rem 2.4rem` tap targets) — no confirmed problem here, but the header's title + 3-item nav flex-wrap behavior at ~390px was not visually confirmed this run (no browser tool available) and is worth a direct screenshot check in a follow-up pass.

## Minor Observations

- No "external link" affordance (icon or label) anywhere on cards despite every single link leaving the site.
- `/projects/` falls back to the generic site-title meta description ("Rory Caraher") for `og:description`/Twitter card since neither the page front matter nor `list.html` sets a page-specific `.Description` — weakens link previews if this page is shared directly with the target peer audience on LinkedIn/Slack.
- `.card:focus-visible` relies solely on the 1px border-color swap plus whatever unsuppressed browser-default outline draws — functional but not deliberately designed, so appearance varies by browser.
- Two large, identically-styled violet headline treatments stack at the very top of the page (`.mg-site-title` + the page's own `<h1>`, both matched by the same CSS rule) — mild tension with DESIGN.md's "violet never decorative" rule, since a static page `<h1>` carries no interactive/state meaning.

## Questions to Consider

- If a 5th project is added, does the 3-up grid or the "≤4 visible choices" cognitive-load ceiling get revisited — or is "curated repo list" implicitly assumed to stay at 4, and if so, is that written down anywhere?
- The stated positioning is systems/reliability depth, but none of the four live project descriptions mention it — should the Projects page carry that positioning at all, or is the CV page meant to do that work by design?
- The nav active-state has apparently never worked on any page of the live site — was this known, or has nobody browsed the deployed site with the nav actually in view since it shipped?
