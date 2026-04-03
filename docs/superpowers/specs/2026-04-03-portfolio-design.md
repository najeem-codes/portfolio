# Portfolio Site — Design Spec
**Date:** 2026-04-03
**Project:** `github.com/najeem-codes/portfolio`

---

## Overview

A full rebuild of Najeem Takiyu-Deen's personal portfolio site as a single-page HTML/CSS/JS application. The site replaces the existing `index.html.html` (wrong extension, job-specific "Why Swarovski" section) with a polished, general-purpose portfolio deployable to GitHub Pages.

---

## Tech Stack

- **Plain HTML/CSS/JS** — single `index.html` file, no build step, no framework
- **Fonts:** Cormorant Garamond (serif headings) + DM Sans (body) via Google Fonts
- **Deployment:** GitHub Pages (`gh-pages` branch or `main` root)
- **Icons:** Inline SVG or Unicode emoji (no external icon library dependency)

---

## Design Direction

**Dark Luxury** — evolution of the existing navy/gold aesthetic.

### Colour Palette
| Token | Value | Usage |
|---|---|---|
| `--navy` | `#1B1B2F` | Dark section backgrounds, hero |
| `--navy-deep` | `#111120` | Footer |
| `--crystal` | `#3A6186` | Accents, timeline dots, section labels |
| `--crystal-light` | `#89A0B4` | Italic hero name, muted text on dark |
| `--gold` | `#C4A35A` | Primary accent, CTA buttons, badges |
| `--gold-light` | `#E8D5A3` | Softer gold on dark backgrounds |
| `--cream` | `#FAF8F4` | Light section backgrounds |
| `--white` | `#FFFFFF` | Cards, credentials section bg |
| `--text` | `#2C2C3E` | Body text on light backgrounds |
| `--muted` | `#6B7280` | Secondary text |
| `--border` | `rgba(58,97,134,0.15)` | Card borders on light bg |

### Typography
- **Display headings:** Cormorant Garamond, weight 300/600, italic variant for name
- **Body / UI:** DM Sans, weight 300/400/500
- **Section labels:** DM Sans 10–11px, letter-spacing 3px, uppercase, `--crystal` or `--gold`

### Animations
- `fadeUp` keyframe on hero elements (staggered 0.1s delays)
- Scroll-triggered `fade-in` class added via IntersectionObserver on section entry
- Hover transitions (0.2s ease) on nav links, skill cards, project cards, credential cards

---

## Sections (top to bottom)

### 1. Sticky Navigation
- Logo: initials "NT" in gold, links to `#hero`
- Links: About · Skills · Projects · Experience · Credentials · Contact
- Behaviour: transparent over hero, becomes white/opaque on scroll past hero
- Mobile: collapses to hamburger menu

### 2. Hero
- Full-viewport dark section (`--navy`)
- Left column: eyebrow label, name (Cormorant Garamond large), title, contact info, skill badges, two CTA buttons ("View Projects" → `#projects`, "Download CV" → PDF link placeholder)
- Right column: circular photo from `C:\Users\najee\Desktop\preview.webp` (copy to `assets/photo.webp`), double-ring gold/crystal border decoration
- Radial gradient orbs as background decoration (existing style preserved)
- Entrance animation: hero-left elements stagger in, hero-right fades up

### 3. About
- Cream background
- Left: professional summary paragraph (from existing file, generalised — removes Swarovski references)
- Right: 3 stat cards (4+ years, BSc., Zürich/Available)

### 4. Skills
- Dark (`--navy`) background, full-width
- 3×2 grid of skill cards: Data Analytics, Reporting & Visualisation, Automation & Systems, Agile & Delivery, Data Management, Collaboration
- Each card: emoji icon, skill name, tag pills

### 5. Projects
- Cream background
- 2-column card grid
- **Card 1 — GhanaSource:**
  - Image: gradient header with 🇬🇭 flag
  - Title: GhanaSource — Product Sourcing Platform
  - Description: Vite + React app for finding products to import and sell in Ghana. Includes cost calculator with Ghana import duties, supplier directory, and sourcing pipeline.
  - Tags: React · Vite · JavaScript
  - Links: "Live Site" → `https://najeem-codes.github.io/ghana-sourcing-app/`, "GitHub" → `https://github.com/najeem-codes/ghana-sourcing-app`
- **Card 2 — Placeholder:** dashed border, "+ More coming soon" centred text, easy to replace later

### 6. Experience
- Cream background
- Vertical timeline with crystal dot + vertical line
- 4 entries (from existing file, all content preserved):
  1. Data Center Operations & Security Officer — Protectas SA at AWS · Dec 2024–Present
  2. IT Service Desk Technician — Altor Equity · Jun 2024–Jan 2025
  3. IT Consultant & Automation Specialist — STECHAD · Dec 2020–Nov 2024
  4. Logistician — Swiss Post · Jul 2020–Jan 2021

### 7. Credentials
- White background
- 3-column card grid with crystal/gold/crystal-light top border accent per card:
  1. BSc. Business Informatics — FHNW Basel (2020–2024)
  2. Scrum Certification — 2025
  3. Power BI & SQL Advanced — In Progress
- Attachment note below: "University certificate, references, and all other certificates available on request."

### 8. Contact
- Dark (`--navy`) background
- Two-column layout:
  - Left: email, phone/location, GitHub button, LinkedIn button
  - Right: contact form (name, email, message, send button)
- Form uses `mailto:` action as a simple no-backend solution
- Social links: GitHub → `https://github.com/najeem-codes`, LinkedIn placeholder

### 9. Footer
- Deep navy (`#111120`)
- Single line: © 2026 Najeem Takiyu-Deen · njmtdeen@gmail.com · Zürich, Switzerland

---

## File Structure

```
portfolio/
├── index.html          ← single file (rename from index.html.html)
├── assets/
│   └── photo.webp      ← copied from Desktop/preview.webp
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-04-03-portfolio-design.md
```

---

## Fixes to Existing File

1. Rename `index.html.html` → `index.html`
2. Remove "Why Swarovski" section entirely
3. Generalise profile summary (remove Swarovski references)
4. Replace base64 placeholder photo with real `assets/photo.webp`
5. Add Projects section
6. Add Contact form section
7. Add scroll-based nav transparency behaviour (JS)
8. Add IntersectionObserver scroll animations (JS)
9. Add mobile hamburger menu (JS)
10. Fix nav: add "Projects" and "Contact" links

---

## Out of Scope

- Backend / form submission service (mailto is sufficient for now)
- React or any framework
- Blog or case study pages
- Dark/light mode toggle
