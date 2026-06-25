# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Status

**No build tooling, no Node — by design.** This is a pure HTML + CSS landing that
uses Tailwind v4 via its **browser CDN** (`@tailwindcss/browser@4`), which
compiles in the page. To work on it, just open [index.html](index.html) in a
browser (or any static server) — there is nothing to install or build.

What exists: the **design system** (colors + typography + icons) and the entry
point [index.html](index.html) (blank body, design system wired up). Don't add
package.json / a Node build unless the user asks — they explicitly chose the
no-toolchain CDN path. (A one-line optional production build is documented in
DESIGN_SYSTEM.md §5 for later.)

## Project goal

A clean, lightweight, responsive landing page built with **Tailwind CSS** that
presents the features of **MicroVend** — an operating system for vending
machines. The author is the OS developer; the site's job is to explain every
feature of the OS. (Note: the product is **MicroVend**, not "SmartVend"; SmartVend
is the broader brand/parent. The logo lives at [assets/logo.svg](assets/logo.svg).)

## Design system (already defined — follow it)

Full spec: [DESIGN_SYSTEM.md](DESIGN_SYSTEM.md). Canonical tokens live in the
`<style type="text/tailwindcss">` block in [index.html](index.html) (Tailwind v4
`@theme`). Standalone visual preview: [design-system.html](design-system.html)
(open in a browser, no build needed).

- **Light theme only.** No dark mode.
- **Colors** derive from [assets/logo.svg](assets/logo.svg): `primary` (blue,
  brand `600 #277BC0`), `accent` (amber, brand `500 #FF9B00`), pure-gray
  `neutral` (wordmark `500`). Accent `500` is **reserved for the primary CTA** —
  don't spread it around.
- **Typography:** **Montserrat** for the logo wordmark, highlighted words, and
  large headings (display/h1/h2); **Inter** for everything else (h3–h6, body,
  UI). Base layer already maps `h1`/`h2` → Montserrat, `h3`+ → Inter.
- **Icons:** **Fluent System Icons** (Microsoft) only, as inline SVG with
  `fill="currentColor"`. Regular variant by default; Filled for active states.

Guiding constraints:
- **Lightweight**: minimal JS, static-first. No build pipeline, no framework.
- **Responsive**: mobile-first; use Tailwind's responsive breakpoint utilities
  rather than custom media queries.
- **Clean**: lean, semantic HTML; let Tailwind utilities + the design tokens do
  the work.
