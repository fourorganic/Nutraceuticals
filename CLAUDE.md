# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project purpose

Marketing landing page for **Fourmidable** (Four Organic) — a nutraceutical product line for poultry farming. The site targets Spanish-speaking B2B clients (poultry producers). Currently one product (liquid curcumin immunomodulator); a second product page is planned. An English version is planned but not yet started.

Live site: https://fourorganic.github.io/Nutraceuticals/ (GitHub Pages — static hosting only, no server-side code)

---

## Build commands

```bash
npm run sass:build   # Compile SCSS → CSS (one-time, no source maps)
npm run sass:watch   # Watch + auto-recompile on save (use during development)
```

**Always edit SCSS source files, never the compiled CSS directly.**

- Source: `scss/styles.scss` and `scss/_variables.scss`
- Output: `css/styles.css` (generated — overwritten on every compile)

---

## Architecture

Single-page site (`index.html`) with one compiled stylesheet (`css/styles.css`).

**SCSS structure — `scss/styles.scss` is organized in order:**
1. Global (body, scroll, section spacing utilities)
2. Navbar (transparent on hero, transitions to opaque on scroll via `.scrolled`)
3. Hero (background image, body layout, KPIs, stats bar)
4. Beneficios, Aplicación, Timeline, Dosage card
5. Resultados comparativos (with/without product comparison)
6. Tecnología
7. CTA / Contacto
8. Footer
9. Utility overrides
10. Responsive (all media queries consolidated at the bottom)

**Bootstrap override pattern:** `scss/_variables.scss` overrides Bootstrap tokens before Bootstrap is imported. Never override Bootstrap variables inside `styles.scss`.

**Responsive breakpoints** (all in `styles.scss` at the bottom):
- `≤ 991.98px` — tablet: navbar collapses, padding scales down
- `≤ 767.98px` — mobile: hero background swaps, layout stacks
- `≤ 575.98px` — small mobile: typography and spacing minimums

**Hero background images:**
- Desktop: `img/Hero-Background.jpg`
- Mobile (≤ 767.98px): `img/Hero-mobile-background.svg` — set via media query in the Responsive section

**JavaScript:** All inline in `index.html` — no separate JS files.
- ROI calculator: reads `#inputAves` and `#inputPrecio`, writes results to `#resultNum`, `#calcResult`, `#calcDetail`
- Scroll animations: Intersection Observer adds `.fade-up` to cards/sections on scroll
- Navbar scroll state: adds `.scrolled` class to `#mainNav` on scroll

---

## Design tokens (`scss/_variables.scss`)

| Token | Value | Use |
|---|---|---|
| `$primary` | `#2e7d32` | Brand green, buttons, accents |
| `$secondary` | `#a7d818` | Lime — all primary CTAs |
| `$accent` | `#f28c00` | Orange highlights |
| `$dark` | `#123c1f` | Near-black text and dark backgrounds |
| `$background` | `#f6f8ef` | Page background (off-white cream) |
| `$green-900/800/700` | `#0d2b12 / #1a4220 / #1f5228` | Dark section backgrounds |

Fonts: **Manrope** (body, loaded via Google Fonts) · **DM Serif Display** (headings)
Buttons: pill-shaped (`border-radius: 50rem`), CTA color is always `$secondary`

---

## Content and copy

- All user-facing copy is in **Spanish**
- Section anchors: `#benefits`, `#aplicacion`, `#resultados`, `#roi`, `#tecnologia`, `#contacto`
- When adding new sections, follow the existing HTML comment block pattern (`<!-- ==== SECTION NAME ==== -->`) and add a corresponding SCSS section with the same name

---

## Planned work

- **Mobile hero layout** — match `img/Hero-mobile-Design.svg` mockup using `img/Hero-mobile-background.svg`
- **Second product page** — new section or page for the upcoming product
- **English version** — future i18n pass; keep copy in clearly identifiable elements (no inline string concatenation in JS)
