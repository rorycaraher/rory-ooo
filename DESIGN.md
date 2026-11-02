---
name: Rory Caraher — Personal Site
description: A dark, minimal engineering logbook — one narrow column of type, with one quiet violet signal marking what's interactive.
colors:
  charcoal-ink: "#18181b"
  pale-fog: "#dadada"
  stone-grey: "#a7a7a7"
  active-violet: "#b175d6"
typography:
  display:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "clamp(2.8rem, 6vw, 3.2rem)"
    fontWeight: 300
    lineHeight: 1.2
    letterSpacing: "-0.02em"
  lead:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "2rem"
    fontWeight: 300
    lineHeight: 1.5
  title:
    fontFamily: "Roboto, \"Helvetica Neue\", Helvetica, Arial, sans-serif"
    fontSize: "1.8rem"
    fontWeight: 300
    lineHeight: 1.4
    letterSpacing: "-0.02em"
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
spacing:
  xs: "0.4rem"
  sm: "0.8rem"
  md: "1.6rem"
  lg: "2.4rem"
  xl: "4rem"
  xxl: "8rem"
components:
  link:
    textColor: "{colors.active-violet}"
    typography: "{typography.body}"
  link-hover:
    textColor: "{colors.pale-fog}"
  site-title:
    textColor: "{colors.pale-fog}"
    typography: "{typography.body}"
  nav-link:
    textColor: "{colors.stone-grey}"
    padding: "0.4rem 0"
  nav-link-active:
    textColor: "{colors.active-violet}"
  row-title:
    textColor: "{colors.active-violet}"
    typography: "{typography.title}"
  row-label:
    textColor: "{colors.stone-grey}"
    typography: "{typography.caption}"
---

# Design System: Rory Caraher — Personal Site

## Overview

**Creative North Star: "Engineering Logbook"**

This site reads as a working record, not a showcase. It is dark, flat, and almost entirely monochrome. One desaturated violet is the only signal, and it means "you can act on this." Nothing competes with it: no shadows, no gradients, no borders, no second accent, no decorative color. That restraint is what makes the site read as credible rather than performed, in service of a platform/infrastructure engineer's positioning.

The page is type and space. Structure comes from size, tone, and whitespace, so anything that is not content or a link has to justify itself. The system is deliberately small enough to hold in your head: four colors, one font weight, one column.

**Key Characteristics:**
- Dark, flat, single-accent: Active Violet means interactive, and nothing else.
- No shadows, rules, dividers, or boxes. Grouping comes from whitespace.
- Light type weight (300) everywhere; restraint over impact.
- One narrow centered column (640px of content), set for comfortable reading.

## Colors

### Primary
- **Active Violet** (`#b175d6`): The only accent. Used for inline links, project and track row titles, the active nav item, and `<strong>`. It is never a background fill, never decoration, and never applied to headings that aren't links.

### Neutral
- **Charcoal Ink** (`#18181b`): Page background, and the only surface color.
- **Pale Fog** (`#dadada`): Primary text, including all headings and the site title, and the hover color for links.
- **Stone Grey** (`#a7a7a7`): Secondary text: row labels and descriptions, CV detail bullets, footer copy, and resting nav links.

### Named Rules
**The One Signal Rule.** Active Violet is the only color allowed to mean "interactive" or "active." It is never used decoratively and never doubled up with a second accent. Page headings are neutral.

**The Hover-Inverts Rule.** Interactive text defaults to the accent and moves to Pale Fog on hover/focus, the opposite of the common "neutral by default, accent on hover" pattern. Preserve this direction. The site chrome (site title, nav, footer) is the exception: it rests neutral so it stays quiet around the content.

## Typography

**Display/Body Font:** Roboto (with `"Helvetica Neue", Helvetica, Arial, sans-serif` fallback). One family for everything; there is no separate display or mono face.

### Hierarchy
- **Display** (`clamp(2.8rem, 6vw, 3.2rem)`, line-height 1.2, letter-spacing -0.02em): `h1`, the page title.
- **Lead** (2rem, line-height 1.5): the homepage's opening paragraph.
- **Title** (1.8rem, line-height 1.4, letter-spacing -0.02em): `h2`, for CV sections and row titles.
- **Body** (1.6rem, line-height 1.6): all running text.
- **Caption** (1.4rem, line-height 1.6): row labels and the footer, in Stone Grey.

### Named Rules
**The Weightless Hierarchy Rule.** Every weight is 300. Never introduce a heavier weight for emphasis, because the font file ships only that weight and bold would compete with the accent. `<strong>` gets color (Active Violet), not boldness.

**The Open Tracking Rule.** Negative letter-spacing belongs to headings only, and is set in `em` so it scales with the type. Never tighten body-sized text; at small sizes it closes up the letterforms.

## Layout

A single centered column: `max-width: 68rem` with `2rem` side padding, for 640px of content. The header, main, and footer all use the same `.container`, so their edges line up. The footer is pushed to the bottom of the viewport on short pages. The type scale is rem-based on a `62.5%` root font-size (`1rem = 10px`).

Vertical rhythm comes from a short scale: `0.8rem` within a group, `1.6rem` between paragraphs, `2.4rem` between list entries, and `4–8rem` between page regions.

## Elevation & Depth

Flat by design. State is conveyed by text color alone, always with a `0.15s ease` transition.

### Named Rules
**The No-Ornament Rule.** Never add `box-shadow`, borders, dividers, background fills, rounded corners, or pill shapes. The one permitted outline is the `:focus-visible` ring, which is an accessibility affordance, not decoration.

## Components

### Links (inline)
- **Default:** Active Violet text, no underline.
- **Hover/Focus:** Pale Fog.

### Header
- **Site title:** body-sized Pale Fog text linking home, Stone Grey on hover. It is the home link, so the menu has no Home entry.
- **Navigation:** horizontal list, `2.4rem` gap, `0.4rem` vertical link padding. Stone Grey at rest, Pale Fog on hover, Active Violet when current.

### Rows (Projects and Music)
- **Partial:** both lists render through `partials/row.html`, so they stay identical.
- **Composition:** the entire row is one link. A Caption label (language, or release date) sits in a fixed `10rem` column at 600px and up and stacks above the title below that. Then a Title in Active Violet, and an optional Body description in Stone Grey with a 2-line clamp.
- **Hover/Focus:** the title moves to Pale Fog.

### CV
Plain markdown lists with the bullets removed. Top-level entries are Pale Fog, and nested detail is Stone Grey. No indentation.

### Footer
Copyright and social links (GitHub / LinkedIn / SoundCloud), Caption size, Stone Grey, in a space-between row that wraps on narrow viewports. Footer links keep their `0.4rem` vertical padding to clear the 24px minimum tap target.

## Do's and Don'ts

### Do:
- **Do** keep Active Violet as the only color that means "interactive" or "active."
- **Do** use whitespace, not lines, to separate things.
- **Do** keep every font-weight at 300.
- **Do** keep the page in the single 640px column.
- **Do** add new list-like sections through `partials/row.html`.

### Don't:
- **Don't** color headings violet unless they are links.
- **Don't** add `box-shadow`, dividers, fills, or rounded corners.
- **Don't** introduce bold or semi-bold weights.
- **Don't** reintroduce a multi-column card grid for Projects; the list is single-column so it scales regardless of project count.
