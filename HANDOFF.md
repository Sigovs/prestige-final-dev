# Prestige Imports — Project Handoff / Notes

Build-free static site (plain HTML + CSS + vanilla JS). Open any `.html` directly,
or serve: `python3 -m http.server 8765`. No framework, no bundler, no build step.

Deployed via **GitHub Pages** from `main` → https://sigovs.github.io/prestige-final-dev/

---

## Pages

| File | Purpose |
|------|---------|
| `index.html` | Home |
| `srp.html` | Inventory / search results |
| `vdp.html` | Vehicle detail |
| `about_our_dealership.html` | About → Our Dealership (subpage) |
| `our_story.html` | About → Our Story (GSAP scrollytelling timeline) |
| `service.html` | Service → Our Services (subpage) |
| `design.html` | Internal design-system reference (no site nav) |

Nav dropdowns: **About** (Our Dealership / Our Story) and **Service** (Service +
Order Parts, 2 columns). Both use `.nav-drop` (hover-open, `<button>`+panel).
Inventory uses the older `.srp-drop` mega-menu. Order-Parts / Schedule / Specials
links are `#` placeholders (pages not built yet).

## CSS layering
`assets/css/tokens.css` (design tokens — colors/type/spacing, single source of truth)
→ `main.css` (home + shared: header, footer, buttons, `.t-*` type ramp, brands,
reviews, nav dropdowns) → `srp.css` / `vdp.css` / **`subpage.css`** (the subpage
template layer). Monochrome editorial system — rhythm comes from layout / scale /
surface / media, not color.

## Subpage template (`assets/css/subpage.css`)
All subpages are built by copying `about_our_dealership.html` and swapping content —
**do not create bespoke one-off pages.** Components: `.subhero`, `.sub-prose` /
`.sub-head`, `.statrow`, `.dept-grid` (+ `--cards` / `--tint` / `--ink` / `--trio`),
`.mediatext` (+ `--flip` / `--portrait`), `.visualbreak` (+ `--tall`, image OR
`<video>`), `.imgcard-grid`, `.contact-form` + `.about-map` (Leaflet, B&W), 
`.feature-band` (photo bg + dark overlay + centered CTA), `.cta-band`, `.pullquote`,
`.statband` (dark radial band), `.timeline` (our_story only).

### Motion
- Reveal-on-scroll: `data-reveal` on a section + `.reveal-up` (rise / cards),
  `.reveal-side` (horizontal staircase / text), `.reveal-left` / `.reveal-right`
  (directional photos). main.js `IntersectionObserver` toggles `.is-visible`;
  CSS nth-child delays make the staircase. `.page-about__main { overflow-x: clip }`
  prevents horizontal-slide scrollbars.
- Parallax: `[data-parallax="<%>"]` on media + CSS `--pscale`; handler in main.js.
- **Section overlap / sticky (service page):** `.section--overlap` lifts a section
  over the previous with a rounded top (`.section--flat-top` = square top, keep the
  lift). Wrap `[sticky section] + [next overlap section]` in `.sticky-stack` and put
  `.section--sticky` on the first — it pins at `top:0` (under the fixed navbar) while
  the next scrolls over it.
- **our_story timeline:** GSAP 3.12 + ScrollTrigger (cdnjs) — giant per-year
  backdrop, clip-path + blur photo reveal, year parallax, pulsing axis node.
  Graceful fallback (all visible) if CDN blocked / reduced-motion.

---

## ⚠️ Deploy + cache (read before editing CSS)

- Push to `main` → Pages rebuilds (~1–2 min). Commit straight to main.
- **CSS/JS are versioned:** `main.css?v=N`, `subpage.css?v=N`, `main.js?v=4`.
  **When you edit main.css or subpage.css you MUST bump `?v=N` on all pages**
  (index, srp, vdp, about_our_dealership, our_story, service, design) or the browser
  serves stale styles. Currently at **`?v=18`**. Subpages also carry a
  `no-cache` meta. Always hard-refresh (**Cmd+Shift+R**) to see changes.
- `.claude/` (agent memory) is gitignored — it does NOT travel with the repo.
- Videos live in `assets/videos/` (some >50MB — GitHub warns but accepts <100MB;
  consider compression / Git LFS for more).

## 📸 Placeholder / duplicate photos still to replace
- `Upgrade_Your_Collection.jpg` — used on **Ride2Revive** bands on both
  about_our_dealership.html and our_story.html (needs real Ride2Revive/charity photo).
- `about.jpg` used twice on about (VB2 + contact photo).
- `spa/auto_hero.jpg` used on about (Auto Spa) and service (Detailing).
- `story/2014_1.jpg` used twice on our_story (timeline 2014 + Next Generation —
  needs a real Brett David portrait).
- `assets/images/story/*` are low-res (~360px, scraped) — swap for hi-res if available.
- Service photos are dedicated & correct (`service/Schedule your service.jpg`,
  `service/Marques We Service.jpg`, `service/service_bay*.jpg`).

## To build the next subpage
1. `cp about_our_dealership.html newpage.html`; rewrite `<main>` with template
   components; keep header / footer / nav verbatim.
2. Add the page to the relevant nav dropdown on all pages; set `is-active`.
3. Pull real photos (client or scrape the live prestigeimports.com page).
4. Bump `?v=N` if you touched CSS. Verify in the browser. Push to main.
