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
| `contact.html` | Contact Us (subpage — channel cards, form + Leaflet map, hours) |
| `index_v2.html` | **Sept 2026 v2 review set** — Home with the September asset/copy updates (new hero videos, Services images, Auto Spa copy, Sell video). `index.html` is untouched. |
| `service_v2.html` | Sept 2026 v2 — Our Services with hero3 video; The Difference / both visual breaks / Marques / Amenities / both CTA bands are **commented out inline** (`<template data-cut>` — delete the tags to restore). `service.html` untouched. |
| `schedule_service_v2.html` | Sept 2026 — Service → Schedule Service lead form: pinned shop-photo rail + 3-chapter form; rail photo follows the chapter (`[data-rail]` in main.js). |
| `concierge_transport_v2.html` | Sept 2026 — landing page for "Beyond the Sale" card 01. Hero → proposition + statrow → three numbered steps on the dark `.statband` → enclosed-transport mediatext → "Request a pickup" form. |
| `oem_parts_v2.html` | Sept 2026 — landing page for card 03. Hero → why OEM → the marque index (reuses the home `.brand-card`) → order form (VIN / part number / fit-it segmented). The four Order-Parts nav items and the index cards all point here and preselect the marque via `[data-fill]` in main.js. |
| `news_events_v2.html` | Sept 2026 — News & Events, built as a **post index, not a calendar**: it is the blog, and AAN's own note says the homepage pulls the four most recent posts from WordPress. Three post kinds share one card and one grid, distinguished by a chip — **Event** (a date the client gave; the weekdays they supplied were checked against the calendar, which is how the years were settled), **Recap** (a photograph from their library, titled by what is in the frame, **deliberately undated** — the EXIF is unreliable: one file carries 2021 on a car announced in 2023, another the 1 Jan default), and **News** (no real content yet, so the card is a visible dashed placeholder rather than an invented article). A lead post sits above the grid. Home `#events` shows the same four events and links here. |
| `news_post_v2.html` | Sept 2026 — the **single-post template**, one article rendered end to end so the furniture can be approved: post head over the photograph (kind chip in cream, `--on-dark`) → lede → subheads → inline figure that breaks wider than the text measure above 1100px → pull quote → `.article__foot` CTAs → "More from the showroom" reusing the index card. **The body copy is simulated and is marked as such in a comment at the top of the file — it is not client copy and must not ship as it stands.** It states no attendance figure, no named quote and no claim about the business, only what the photographs show, so nothing in it can be published by accident as fact. Every card on the index links here; in the CMS the chip, date, hero and body come from the post record and News/Event posts use the same template. |
| `specials_v2.html` | Sept 2026 — Service → Service / Parts Specials. **The empty state is the designed state:** the live page has no offers and dead-ends on "check back soon", so this one says so plainly, then routes on (standing advantages → notify form). `.special` is the offer card the dealer fills; the paste-in markup template sits in an HTML comment in the page. Every offer must carry its own end date. |
| `lamborghini_parts_v2.html` · `pagani_parts_v2.html` · `karma_parts_v2.html` | Sept 2026 — a counter page per marque, generated from one spine (see the generator kept in the session scratchpad; content lives in a dict at the top). Hero → why the authorized source → model coverage (`.qa--models`) → order form with the marque in a hidden field → the other marques. **Lotus has no page here** — it already has a store. |
| `warranty_v2.html` | Sept 2026 — landing page for card 04. Hero → why coverage matters on an exotic → a five-question editorial Q&A (`.qa`, the set's only long-form list) → coverage enquiry form. **Names no provider, plan, term or price — we have none.** |
| `collision_restoration_v2.html` | Sept 2026 — landing page for card 02. Hero → why certification → connected 4-up coverage grid → paint mediatext → "Request an estimate" form (carries the insurance-claim `.segmented`). |
| `design.html` | Internal design-system reference (no site nav) |

Nav dropdowns: **About** (Our Dealership / Our Story) and **Service** (Service +
Order Parts, 2 columns). Both use `.nav-drop` (hover-open, `<button>`+panel).
Inventory uses the older `.srp-drop` mega-menu. Across the v2 set the Service
column is fully wired — Order Parts, Schedule Service and Specials all resolve —
and the nav and footer are identical on every v2 page; regenerate them from one
source if they ever drift.

**Service landing pages (Sept 2026).** The client asked for a page per "Beyond
the Sale" element. All four cards are built and are links (caret affordance). Both new pages reuse the existing subpage components
(`.subhero`, `.sub-prose`, `.statrow`, `.statband` + `.dept-grid--ink`,
`.mediatext`, `.contact-form`, `.sched__facts`); no decorative full-bleed breaks,
because the client cut exactly those from Our Services as "adding no value".
Copy facts came from the live site's `clp-*` pages, rewritten — the live SEO copy
itself was not carried over. **Still missing from the client:** the enclosed-transport coverage
area (so no page states a radius — the form asks where the car is instead) and
every warranty specific: provider, plan names, terms, transferability, price.
`warranty_v2.html` is written to be honest without them — it explains and invites
the conversation — but it is not a product page until those arrive.

The footer's Service column is identical on all eight v2 pages; regenerate it from
one source if it drifts, which it did twice while these pages were being added.

**The v2 set is walkable (Sept 2026).** Every page in it links only to other v2
pages, and a crawl from `index_v2.html` reaches all sixteen with no broken target:
`srp_v2`, `vdp_v2`, `about_our_dealership_v2`, `our_story_v2` and `contact_v2` are
link-only copies of the originals — same content, nav and footer repointed — so a
reviewer cannot fall out of the set and get stranded on a page whose nav predates
the September round. Regenerate them from the originals if the originals change.

**Still dead by design** (no page exists yet, listed so nobody hunts for a bug):
Privacy / Terms / Sitemap, the Store and Research nav items, and Explore Auto Spa / Marine / Prestige Energy. The seven
marque tiles point at `srp_v2.html?make=…` for now — the inventory ignores the
query, so it lands on the full list; the client's tracker defers real brand pages
until after launch.

**v2 review set (Sept 2026):** `index_v2.html`, `service_v2.html` and
`schedule_service_v2.html` link only to each other (logo → index_v2, Service →
service_v2, Schedule → schedule_service) so a reviewer stays inside v2; the
original pages are byte-identical to before the update (they stay on
`subpage.css?v=19` and never link `v2.css`; the v2 pages are on `?v=21`).
`assets/css/v2.css` is the v2-only layer: the Services-card links plus the
contrast / 14px-floor corrections inside that block (`.service__body` was
12.5px at 3.63:1). To go live, copy the
v2 files over the originals and point their links back at `index.html` /
`service.html`. Raw client files are in `UPDATES SEPTEMBER 2026/` (untracked).

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
`.contact-split` (form | map), `.field--row` (2-up inputs), `.segmented`
(connected Call/Text/Email radio toggle), `.hours` (2-col hours table),
`.dept__phone` (click-to-call in `.dept` cards),
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
- **CSS/JS are versioned:** `main.css?v=N`, `subpage.css?v=N`, `main.js?v=N`.
  **When you edit main.css or subpage.css you MUST bump `?v=N` on all pages**
  (index, srp, vdp, about_our_dealership, our_story, service, design) or the browser
  serves stale styles. Currently `main.css?v=19`; v2 pages carry `subpage.css?v=20` + `main.js?v=6` (additive CSS/JS for the schedule page). Subpages also carry a
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
