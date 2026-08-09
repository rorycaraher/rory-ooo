---
name: Rory Caraher — Personal Site
description: A dark, minimal engineering logbook — CV, curated projects, and one quiet violet signal marking what's interactive.
colors:
  charcoal-ink: "#18181b"
  pale-fog: "#dadada"
  stone-grey: "#a7a7a7"
  graphite: "#4e4e4e"
  active-violet: "#b175d6"
typography:
  display:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "clamp(3.2rem, 8vw, 5rem)"
    fontWeight: 300
    lineHeight: 1
    letterSpacing: "-0.1rem"
  headline:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "clamp(2.4rem, 6vw, 3.6rem)"
    fontWeight: 300
    lineHeight: 1.2
    letterSpacing: "-0.1rem"
  title:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "clamp(1.8rem, 4.5vw, 2.8rem)"
    fontWeight: 300
    lineHeight: 1.3
    letterSpacing: "-0.1rem"
  body:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "1.6rem"
    fontWeight: 300
    lineHeight: 1.6
  caption:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "1.4rem"
    fontWeight: 300
    lineHeight: 1.6
  label:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "1.2rem"
    fontWeight: 300
    letterSpacing: "0.05em"
    textTransform: "uppercase"
spacing:
  xs: "0.8rem"
  sm: "1.2rem"
  md: "1.6rem"
  lg: "2.4rem"
  xl: "3.2rem"
  xxl: "6.4rem"
components:
  link:
    textColor: "{colors.active-violet}"
    typography: "{typography.body}"
  link-hover:
    textColor: "{colors.pale-fog}"
  nav-link:
    textColor: "{colors.stone-grey}"
    padding: "0.8rem 1.2rem"
  nav-link-active:
    textColor: "{colors.active-violet}"
  project-row:
    textColor: "{colors.pale-fog}"
    borderColor: "{colors.graphite}"
    padding: "2.4rem 0"
  project-row-hover:
    borderColor: "{colors.active-violet}"
    padding: "2.4rem 0"
  project-lang:
    textColor: "{colors.stone-grey}"
    typography: "{typography.label}"
  project-lang-hover:
    textColor: "{colors.active-violet}"
---

# Design System: Rory Caraher — Personal Site

## Overview

**Creative North Star: "Engineering Logbook"**

This site reads as a working record, not a showcase. It is dark, flat, and almost entirely monochrome — one deliberately desaturated violet is the system's only signal, spent on links, the active nav item, and project-row hover, and nowhere else. Nothing competes with it: no shadows, no gradients, no second accent, no decorative color. That restraint is the point — it's what makes the site read as credible rather than performed, in service of a platform/infrastructure engineer's positioning (durable, precise, no ornament for its own sake).

Interaction is tactile but minimal: hover and focus states are real (border and text color shift, always with a transition), but the vocabulary is deliberately small — color and border are the only levers pulled. The logbook metaphor extends to typography and layout too: light-weight type (300 everywhere, including headings), tight negative letter-spacing on headings, and a single centered content column. Nothing asks to be noticed except the content itself and the one color that means "this is interactive."

**Key Characteristics:**
- Dark, flat, single-accent — Active Violet is the only color allowed to mean "interactive."
- No shadows anywhere; depth, when it exists at all, is conveyed by border-color shifts, not elevation.
- Light type weight (300) even in display sizes — restraint over impact.
- One centered column (max 1025px), no sidebars, no card-grid layouts — even the Projects list is single-column rows.

## Colors

A near-monochrome dark palette (charcoal background, two greys for text hierarchy, one border grey) with a single violet accent that carries all interactive meaning.

### Primary
- **Active Violet** (`#b175d6`): The system's only accent. Used for link text (default state, not hover), the active nav item's label and underline, `h1` heading color, `<strong>` emphasis inside list items, and the border/label color a project row shifts to on hover/focus. It never appears as a background fill or decoration — only as text/border color marking something live or important.

### Neutral
- **Charcoal Ink** (`#18181b`): Page background. The only surface color in the system — there is no secondary/elevated surface tone.
- **Pale Fog** (`#dadada`): Primary body text color, and the color links and nav items shift to on hover/focus (i.e. hover moves *away* from the accent toward this neutral, not toward a brighter version of the accent).
- **Stone Grey** (`#a7a7a7`): Secondary text — project descriptions, project language labels, footer copy, default (non-hover, non-active) nav link color.
- **Graphite** (`#4e4e4e`): The only border color in the system — project row dividers, the footer's top rule.

### Named Rules
**The One Signal Rule.** Active Violet is the only color allowed to mean "interactive" or "active." It is never used decoratively, never as a fill, and never doubled up with a second accent.

**The Hover-Inverts Rule.** Interactive text defaults to the accent color and moves to a neutral (Pale Fog) on hover/focus — the opposite of the more common "neutral by default, accent on hover" pattern. Preserve this direction; don't flip it.

## Typography

**Display/Body Font:** Roboto (with `"Helvetica Neue", Helvetica, Arial, sans-serif` fallback) — a single family for everything; there is no separate display or mono face.

**Character:** Light and quiet. Every weight in the system is 300 (including `h1`–`h3`), so hierarchy comes entirely from size and negative letter-spacing, never from boldness. This is deliberate: bold type would compete with the one accent color for attention.

### Hierarchy
- **Display** (300, `clamp(3.2rem, 8vw, 5rem)` / 32–50px, line-height 1, letter-spacing -0.1rem): `h1` only — page title, colored Active Violet.
- **Headline** (300, `clamp(2.4rem, 6vw, 3.6rem)` / 24–36px, line-height 1.2, letter-spacing -0.1rem): `h2`.
- **Title** (300, `clamp(1.8rem, 4.5vw, 2.8rem)` / 18–28px, line-height 1.3, letter-spacing -0.1rem): `h3` — project row titles, section subheadings.
- **Body** (300, 1.6rem/16px, line-height 1.6, fixed — no fluid scaling): all running text, including project descriptions (in Stone Grey).
- **Caption** (300, 1.4rem/14px, line-height 1.6, fixed): footer copy, in Stone Grey.
- **Label** (300, 1.2rem/12px, letter-spacing 0.05em, uppercase, fixed): the project row's language tag, in Stone Grey (Active Violet on hover/focus).

### Named Rules
**The Weightless Hierarchy Rule.** Never introduce a heavier font-weight to create emphasis. Hierarchy is built from size, line-height, and negative letter-spacing only; `<strong>` gets color (Active Violet), not boldness (`font-weight: normal`).

**The Fluid Heading Rule.** Headings (`h1`–`h3`, and the header's `.mg-site-title` which mirrors `h1`) scale with `clamp()` between a mobile floor and the desktop ceiling — never a fixed size. Body and label text stay fixed; only the three heading roles are fluid.

## Layout

A single centered column, `max-width: 1025px`, with `1rem` horizontal padding (`.mg-container`) — no sidebars, no asymmetric or multi-column page layouts anywhere on the site. The type scale is rem-based on a `62.5%` root font-size (so `1rem = 10px`), which keeps all sizing in the CSS legible as near-pixel values.

The Projects page is a single-column list (`.project-list`), not a grid: each project is a full-width row (`.project-row`) stacked vertically, separated by hairline Graphite dividers, with the language label and title/description arranged side-by-side above 769px and stacked below it. Vertical rhythm is coarse and consistent: `3.2rem` above major sections, `6.4rem` above the footer, `1.6rem`/`2rem` between smaller elements. There is no dense or compact mode — spacing stays generous throughout.

Headings scale fluidly with viewport width (see Typography's Fluid Heading Rule) so the type system participates in the same responsive behavior as the grid — a heading never dominates a narrow viewport the way a fixed desktop size would.

## Elevation & Depth

Flat by design — there are no shadows anywhere in the system. Depth and state are conveyed entirely through border-color and text-color shifts (Graphite → Active Violet on project-row hover; Stone Grey → Active Violet on active nav), not through layering, blur, or lift.

### Named Rules
**The No-Shadow Rule.** Never introduce `box-shadow` to indicate elevation or hover state. State changes are color-only (border and/or text), always with a short transition (`0.15s ease` is the established duration).

## Shapes

No rounding anywhere in the system — every corner is square. Borders are hairline (`0.1rem`/1px, Graphite) and are the system's entire form language — nav uses a `0.2rem` bottom border as an underline indicator for the active item, and project rows use the same hairline as a divider that shifts to Active Violet on hover/focus rather than a filled or pill-shaped tab. No pill shapes, no rounding, no clipping or asymmetric geometry anywhere.

## Components

Interaction across the system is tactile but minimal: every stateful component responds with a real, transitioned color change, but the vocabulary never grows beyond border-color and text-color.

### Links (inline)
- **Default:** Active Violet text, no underline.
- **Hover/Focus:** shifts to Pale Fog (moves toward neutral, not a brighter accent).

### Navigation
- **Style:** horizontal flex list, `1.6rem` gap between items; each link `0.8rem 1.2rem` padding.
- **Default:** Stone Grey text.
- **Hover:** Pale Fog text.
- **Active:** Active Violet text with a `0.2rem` solid Active Violet bottom border (the underline is the active-state indicator, not a background fill).

### Project Rows
- **Corner Style:** none — square, no radius.
- **Background:** none — inherits the page's Charcoal Ink; rows are defined by their divider, not a filled surface.
- **Divider:** `0.1rem` solid Graphite bottom border per row (the list itself opens with the same hairline as a top border), shifting to Active Violet on hover/focus-visible (`border-color 0.15s ease`).
- **Shadow Strategy:** none — see Elevation & Depth.
- **Padding:** `2.4rem 0` (mobile), `3.2rem 0` (≥769px) — vertical only; rows are full-width, no horizontal inset beyond the page container.
- **Composition:** language Label on the left (fixed `12rem` column ≥769px, stacked above the title on mobile) shifting Stone Grey → Active Violet on hover/focus, title (Title-scale) and description (Body-scale, Stone Grey, 2-line clamp) on the right.
- **Behavior:** the entire row is the link (project name + description); no boxed card, no per-item background.

### Footer
- **Style:** `0.1rem` solid Graphite top border, `3.2rem 1rem` inner padding, `6.4rem` margin above it. Copyright and social links (GitHub / LinkedIn / SoundCloud) in a space-between flex row, wrapping on narrow viewports. Links are Stone Grey by default, Pale Fog on hover — footer links follow the nav's neutral-hover pattern, not the inline-link accent-default pattern.
- **Touch target:** footer links carry `0.4rem 0` vertical padding (on top of their text) to clear the 24px minimum tap-target size — don't strip this padding even though it's visually invisible at rest.

## Do's and Don'ts

### Do:
- **Do** keep Active Violet as the only color that means "interactive" or "active" — never introduce a second accent hue.
- **Do** use color-only, transitioned state changes (`0.15s ease` border/text-color) for hover and focus — this is the system's entire interaction vocabulary.
- **Do** keep every font-weight at 300, including headings; build hierarchy from size and negative letter-spacing instead.
- **Do** keep the page in a single centered column (`max-width: 1025px`).

### Don't:
- **Don't** add `box-shadow` anywhere — depth is conveyed by border-color and text-color only.
- **Don't** fill rows, nav items, or buttons with a background color on hover or active state — every existing state change is a border/text color shift, never a fill.
- **Don't** introduce bold or semi-bold weights for emphasis; use Active Violet color on `<strong>` instead.
- **Don't** round corners or introduce pill shapes — the system has no rounding anywhere.
- **Don't** reintroduce a multi-column card grid for Projects — the list is deliberately single-column so it scales cleanly regardless of project count.
