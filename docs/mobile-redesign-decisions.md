# Mobile redesign (Portfolio26.2) — decisions & filled-in details

Build of the new **mobile** homepage from the Figma file `Portfolio26.2`
(`nWTWFYf9NMGkwOMvAei7ge`). Ships as the experience below `768px`; the legacy
desktop site is unchanged and still renders at `≥768px`. Everything below was
decided during the build — either confirmed with Stephen or filled in and
documented per his request ("document all decisions / edge cases").

## Confirmed with Stephen
- **Portfolio gate** keeps password `G00se`; unlock is **remembered for the
  browser session** (`sessionStorage`), so no re-prompt on reload. Mobile and
  desktop gates share one key (`portfolioUnlocked`).
- **Case-study modal** is **closeable-only** (no live case-study pages yet). It
  keeps the password field + "Unlock the case study" button for design fidelity,
  but submitting shows a friendly "coming soon" message. X / tap-outside / Esc
  closes back to the homepage.
- **Contact** — all contact / reach-out links point to
  `mailto:stephen.aase@gmail.com` ("Get in touch", footer CTA, "No password?
  Reach out to connect").

## Filled in (design/engineering decisions)
1. **Palette divergence is intentional.** The mobile design uses the new
   purple/violet system; the legacy desktop keeps the warm/rust tokens until the
   desktop pass. New tokens were added **additively** to `colors_and_type.css`
   (warm tokens untouched) and are authored as the eventual *site-wide* system.
2. **Mobile-first, single canonical DOM.** New markup uses role-based class
   names (`.m2-hero`, `.m2-nav`, …), not viewport names, and is authored
   mobile-first so tablet/desktop become additive `min-width` layers later
   (breakpoint tokens `--bp-sm/md/lg/xl` are defined). The legacy desktop block
   is retained only until that pass, then retired.
3. **Breakpoint** — the new experience renders `< 768px` (reuses the site's
   existing mobile threshold); desktop is unchanged this release.
4. **Fonts** — the design uses **Roboto Slab + Roboto**, which had broken
   `@font-face` paths in the repo. Both are now self-hosted as variable WOFF2
   in `/fonts` (matching the existing self-hosted pattern) and preloaded.
5. **AI-leadership cards are NOT gated case studies.** Their own CTA reads
   "Case study coming soon", so they are presentational; only the three
   **Selected work** cards open the case-study modal.
6. **Case-study covers + AI illustrations** are exported PNGs from Figma
   (`/assets`); card copy, titles, metrics, and CTAs are live HTML/CSS text for
   crispness and accessibility. The whole work card is the tap target.
7. **Redacted metrics** — Walmart and Design-Systems cards show pixelated/
   redacted metric values exactly as designed (confidential numbers); rendered
   as a CSS checkerboard in the card's theme color. Realtor shows real values
   (L3+, 25%).
8. **Carousels** (stats, testimonials, AI leadership) use native CSS scroll-snap
   for momentum swipe, with pagination dots that track the active card via
   `IntersectionObserver`. Testimonial cards snap to `start` (left gutter);
   single-up cards snap centered.
9. **Nav → section map**: Testimonials→`#m2-testimonials`, Case studies→
   `#m2-work`, About me→`#m2-about`, AI leadership→`#m2-ai`, Get in touch→
   `#m2-contact`. Tapping a link closes the drawer, then smooth-scrolls.
10. **Résumé link** (footer) currently points to LinkedIn as a stand-in —
    **replace with a real résumé URL/PDF when available.**
11. **Device status bar** (the `9:41` / signal-icon chrome in the Figma frames)
    is intentionally **omitted** — the real browser provides it.
12. **Motion & accessibility** — scroll-reveal (below-the-fold fade+rise),
    drawer/modal transitions, and the hamburger↔X animation are all disabled or
    reduced under `prefers-reduced-motion`. Modals/drawer are focus-trapped with
    `aria-modal`, Esc/scrim close, and scroll-lock without layout shift.
13. **Guiding-principle icons** are the exact Walmart Living Design pictograms
    exported from Figma (`/assets/icon-*`).

## Still open / next steps
- Real **Résumé** link (see #10).
- **Desktop & tablet** breakpoints: add `min-width` layers to this DOM using the
  new tokens, then remove the legacy `.stage`/`.page` block and warm tokens.
- Optional: revisit the 8 npm-audit advisories (dependency-only; don't affect
  this static build).
