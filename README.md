# Prestige Imports — Website (Final Handoff)

Static, build-free front-end. Plain HTML + CSS + vanilla JS. Open any `.html`
directly in a browser, or serve the folder (`python3 -m http.server`).

## Pages
| File | Purpose |
|------|---------|
| `index.html` | Home |
| `srp.html`   | Search Results / Inventory listing |
| `vdp.html`   | Vehicle Detail page |
| `design.html`| Design-system reference (tokens, type, buttons) — not a public page |

## Structure
```
index.html · srp.html · vdp.html · design.html
assets/
  css/
    tokens.css   ← design tokens (SINGLE SOURCE OF TRUTH: color, type, spacing, motion)
    main.css     ← home + shared components (header, hero, footer, buttons, cards…)
    srp.css      ← SRP-only styles
    vdp.css      ← VDP-only styles
  js/
    main.js      ← header, hero slider, scroll reveals, interactions
    search.js    ← home search widget
    search5.js   ← SRP filtering / sorting
    vdp.js       ← VDP gallery
  images/        ← only assets actually referenced by the pages
  videos/        ← hero + section background videos
```

## How it loads
Every page includes, in `<head>`, in this order:
1. Google Fonts — **Plus Jakarta Sans** (display/headings) + **Inter** (body/UI).
2. Phosphor Icons (CDN).
3. `assets/css/tokens.css` — then `main.css` (+ `srp.css` / `vdp.css` as needed).

## Conventions
- **Tokens first.** Never hardcode a color/space/font — use the `--token`. Change it in `tokens.css` and it updates everywhere.
- **BEM** naming: `.block__element--modifier`.
- **Buttons:** `.btn` + `.btn--solid` / `.btn--on-dark` / `.btn--ghost`.
- **Eyebrow labels:** `.eyebrow-stamp` (`--light` on dark surfaces).
- One responsive token override (`--section-py`, `--header-h`) lives in `main.css` under `@media (max-width: 960px)`.

## Notes for the developer
- Brand cards / hero brand links point to `#` placeholders — wire to Brand CLP pages when available.
- Inventory counts, vehicle data, reviews, and events are static placeholders — connect to the live data source.
- `favicon.ico` not included — add one to remove the console 404.
