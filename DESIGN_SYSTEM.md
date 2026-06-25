# MicroVend — Design System

Design tokens for the MicroVend landing page (an operating system for vending
machines). **Light theme only.** Canonical source of truth is the
`<style type="text/tailwindcss">` block in [index.html](index.html) (Tailwind v4
`@theme`, loaded via the browser CDN — no build step). This document explains the
*why* and how to use the tokens.

---

## 1. Color

### Where the palette comes from
The brand [logo](assets/logo.svg) defines three colors:

| Role in logo | Hex | Notes |
|---|---|---|
| Mark (primary) | `#277BC0` | Blue |
| Mark (accent) | `#FF9B00` / `#FEB139` | Amber / orange |
| Wordmark | `#707070` | Neutral gray (anchors the gray scale) |

This is a **complementary blue + orange** pairing — the same logic the largest
tech brands rely on. Blue dominates technology branding (IBM, Intel, Samsung,
HP, Dell, PayPal, Stripe, LinkedIn, Meta) because it reads as **trust,
reliability, infrastructure** — exactly the message for an OS. The warm amber is
the high-contrast counterpoint (cf. Amazon, Firefox, HubSpot) that gives CTAs
energy and makes them pop against the blue. The brand already lands on a proven
scheme; the system just extends it into full tonal scales.

### Tonal scales
Each scale runs 50 → 950. The **brand anchors** are highlighted.

**Primary — blue** (`primary-*`)
`50 #eff6fc` · `100 #d6e9f7` · `200 #aed3ef` · `300 #79b6e2` · `400 #4496d2` ·
`500 #2a82c8` · **`600 #277bc0` (brand)** · `700 #21649c` · `800 #1f527e` ·
`900 #1d4567` · `950 #122b41`

**Accent — amber** (`accent-*`)
`50 #fff8eb` · `100 #feefc8` · `200 #fedc8b` · `300 #fec95a` ·
**`400 #feb139` (brand light)** · **`500 #ff9b00` (brand)** · `600 #e07c00` ·
`700 #b95b03` · `800 #96470b` · `900 #7b3b0e` · `950 #471d02`

**Neutral — gray** (`neutral-*`, pure gray to match the wordmark)
`50 #fafafa` · `100 #f5f5f5` · `200 #e5e5e5` · `300 #d4d4d4` · `400 #a3a3a3` ·
**`500 #737373` (≈ wordmark)** · `600 #525252` · `700 #404040` · `800 #262626` ·
`900 #171717` · `950 #0a0a0a`

### Semantic & surface aliases
| Token | Value | Use |
|---|---|---|
| `background` | `#ffffff` | Page background |
| `surface` | `#fafafa` | Cards, raised blocks |
| `surface-alt` | `#f4f8fb` | Blue-tinted alternating sections |
| `border` | `#e5e5e5` | Hairlines, dividers |
| `text` | `#171717` | Primary text |
| `text-muted` | `#525252` | Secondary text |
| `text-subtle` | `#737373` | Captions, placeholders |
| `success` | `#16a34a` | (soft `#dcfce7`) |
| `warning` | `#d97706` | (soft `#fef3c7`) |
| `danger` | `#dc2626` | (soft `#fee2e2`) |
| `info` | `#277bc0` | (soft `#d6e9f7`) |

### Usage rules
- **Primary `600`** = default brand blue: links, primary surfaces, icons.
- **Accent `500`** = reserved for CTAs and the single most important action on a
  view. Don't dilute it — its power is scarcity. Use `accent-600` for hover.
- Body text on white: `text` (`neutral-900`). Secondary: `text-muted`.
- Keep large fills neutral/white; let blue and amber carry meaning, not area.
- Contrast: `primary-600` and `accent-600`+ pass AA on white for normal text;
  `accent-500` is for large text / UI fills, not small body copy on white.

---

## 2. Typography

Two families, with a hard rule:

> **Montserrat** — logo wordmark, highlighted words, and **large headings**
> (display, h1, h2).
> **Inter** — everything else: h3–h6, body, UI, buttons, labels, captions.

| Token | Family | Size (fluid) | Weight / LH | Use |
|---|---|---|---|---|
| `text-display` | Montserrat | 40 → 72px | 800 / 1.05 | Hero headline |
| `text-h1` | Montserrat | 32 → 48px | 700 / 1.1 | Page / section title |
| `text-h2` | Montserrat | 24 → 36px | 700 / 1.15 | Section title |
| `text-h3` | Inter | 24px | 600 / 1.25 | Sub-section |
| `text-h4` | Inter | 20px | 600 / 1.3 | Card title |
| `text-body-lg` | Inter | 18px | 400 / 1.7 | Lead paragraph |
| `text-body` | Inter | 16px | 400 / 1.65 | Default body |
| `text-small` | Inter | 14px | 400 / 1.5 | Secondary |
| `text-caption` | Inter | 12px | 500 / 1.4 | Labels, meta |

Weights loaded: Montserrat 600/700/800, Inter 400/500/600/700.

### Highlights
For an accented phrase inside a headline use:
- `.text-highlight` — Montserrat 700 in `accent-500`.
- `.text-gradient` — Montserrat 800 with a blue→amber gradient clip.

Defaults are wired in the base layer: `h1`/`h2` automatically render in
Montserrat, `h3`–`h6` in Inter. Apply `.font-display` to opt any element into
Montserrat (e.g. the logo wordmark).

---

## 3. Icons

**Library: [Fluent System Icons](https://github.com/microsoft/fluentui-system-icons)** (Microsoft). One icon set everywhere — no mixing.

- **Variants:** use **Regular** for default UI; **Filled** only for active/selected
  states or small emphasis marks. Don't mix outline sets from other libraries.
- **Delivery:** prefer **inline SVG** with `fill="currentColor"` so icons inherit
  text color (then `text-primary-600`, `text-accent-500`, etc. just work). For a
  static landing this keeps the page light — pull only the SVGs you use rather
  than shipping the whole font/package. (`@fluentui/react-icons` is for React apps;
  this landing isn't one unless that changes.)
- **Sizes:** Fluent ships at 12/16/20/24/28/32/48. Map to UI:
  inline-with-text `16` · buttons/nav `20` · feature cards `24–32` · hero/marketing `48`.
- **Color:** icons carry meaning through `primary-600` (default) and `accent-500`
  (reserved, like CTAs). Decorative icon tiles use a `primary-50` background +
  `primary-600` glyph (see the feature card in the preview).
- **A11y:** decorative icons get `aria-hidden="true"`; meaningful standalone icons
  get an `aria-label`.

```html
<!-- inline SVG, inherits color + size from the parent -->
<span class="text-primary-600 [&>svg]:size-6">
  <!-- paste a Fluent "Regular" 24 SVG here, set fill="currentColor" -->
</span>
```

> The preview (`design-system.html`) uses emoji as placeholders; swap them for
> Fluent SVGs in real components.

---

## 4. Other tokens

**Radius:** `sm .375rem` · `md .625rem` · `lg 1rem` · `xl 1.5rem`
**Shadow:** `soft` (subtle card lift) · `pop` (blue-tinted, for hovered CTAs)

---

## 5. Usage

Pure HTML + CSS, **no toolchain**. [index.html](index.html) loads Tailwind v4
from the browser CDN and defines all tokens inline:

```html
<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
<style type="text/tailwindcss">
  @theme { /* color / font / size tokens */ }
  @layer base { /* h1,h2 → Montserrat; h3+ → Inter */ }
  @layer components { .text-highlight { … } .text-gradient { … } }
</style>
```

Then use Tailwind utilities with the brand tokens directly:

```html
<h1>Операционная система для <span class="text-highlight">вендинга</span></h1>
<button class="bg-accent-500 hover:bg-accent-600 text-white rounded-md px-5 py-3">
  Попробовать
</button>
<section class="bg-surface-alt text-text">…</section>
```

> The IDE may flag `@theme` / `@layer` as "unknown at-rule" — that's the editor's
> CSS linter, not an error; the Tailwind browser build processes them at runtime.

**Going to production?** The CDN compiles in the browser (fine for a simple
landing, but adds runtime cost + a brief FOUC). To ship a static stylesheet, copy
the `<style>` block into a `.css` file, prepend `@import "tailwindcss";`, and run
`npx @tailwindcss/cli -i in.css -o out.css --minify` — then replace the CDN
`<script>` with a `<link>` to the output. (This is the only step that needs Node,
and it's optional.)

Preview every token in the browser (also no build): open
[design-system.html](design-system.html).
