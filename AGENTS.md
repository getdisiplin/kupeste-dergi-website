# AGENTS.md

## Project

Static website for **Küpeşte** — Turkish literary/arts magazine, 54 issues. No package.json, no build system.

## Key Files

| Path | Purpose |
|---|---|
| `index.html` | Main site (~1003 lines, self-contained, Tailwind CDN + GSAP 3.12.5) |
| `index-backup.html` | Earlier dark-theme variant (588 lines) |
| `pdfjs/web/viewer.html` | PDF.js viewer (v4.5, Dec 2023) |
| `pdfjs/build/pdf.worker.mjs` | Worker entry for PDF rendering |
| `Kağıt.jpg` | Paper texture overlay (723×1024) |
| `SKILL.md` | `site-teardown` skill — reverse-engineer live sites |

## Architecture

- **Single-page app**: Fixed header, card carousel (cover images), grid view, bottom nav bar, modals (About + PDF reader)
- **JS**: Vanilla ES5 IIFE (no modules). GSAP for animations, pointer-drag for carousel, keyboard/wheel navigation
- **Index reversed**: Array index 0 = sayi 54 (newest first). `getRealIssueNum(i)` reverses.
- **PDF reader**: `pdfjs/web/viewer.html?file=../../Küpeşte/sayilar/Kupeste_dergi_Sayi_{NN}.pdf`
- **Grid toggle**: Switches carousel ↔ grid layout, grid built dynamically from cover images
- **Hash routing**: `#sayi-{NN}` for deep-linking issues

## Asset Sources (all verified)

| Asset | Pattern | Count |
|---|---|---|
| Covers | `Küpeşte/kapak/sayi{01-54}.jpg` | 54 |
| PDFs | `Küpeşte/sayilar/Kupeste_dergi_Sayi_{01-54}.pdf` | 54 |
| Logo | `Küpeşte/kupeste.png` (1500×680) | 1 |
| Texture | `Kağıt.jpg` (723×1024) | 1 |

## Commands

```bash
# Serve locally
npx serve . --no-clipboard -l 3000

# Or with Python
python3 -m http.server 3000
```

## Stale / Missing Items (Do Not Use)

- `serve.mjs` and `screenshot.mjs` — referenced in OPENCODE.md but don't exist
- `brand_assets/` — does not exist
- Puppeteer/Chrome paths in OPENCODE.md — Windows paths from another machine

## Style Constraints (from OPENCODE.md, enforced in code)

- Custom brand color (`#6b4a2e` accent, `#f6f2ea` bg), never Tailwind blue/indigo
- Layered color-tinted shadows, never flat `shadow-md`
- Playfair Display (serif) for headings + Inter (sans) for body + JetBrains Mono (mono) for UI
- SVG grain/noise overlay for texture
- Only animate `transform` + `opacity`, never `transition-all`
- Every clickable: hover, focus-visible, active states
- Surface layering: base → elevated → floating

## Before Frontend Changes

Invoke `frontend-design` skill before writing any UI code.
