# Agent instructions for this repo

This repo is the marketing website for Fourth Light Farm Construction, LLC (FLFC), a for-profit general
contracting/construction company. FLFC is affiliated by donation with Fourth Light Farm, a sustainable-agriculture
nonprofit (see the separate `flf` repo) — FLFC is its own business, not the nonprofit itself. The person requesting
changes is likely non-technical. Optimize for the smallest, safest edit that achieves what they asked for, and
explain what you changed in plain terms afterward.

## What this site is

Static HTML pages. No framework, no build step, no package manager, no dependencies to install.

- `index.html` — the main page: hero, about, services, community impact, and contact sections, plus a small inline
  `<script>` at the bottom for the mobile nav toggle and smooth scrolling.
- `portfolio.html` — a gallery page of past projects. 4 real photo cards + 1 "more coming soon" card (see Known
  placeholders below). Each real photo sits in a `<button class="portfolio-thumb">` — clicking it opens a lightbox
  overlay (`#lightbox` markup near the end of the body, styles in `theme.css` under "Lightbox / Slideshow", JS at the
  bottom of the file) that lets visitors step through all `.portfolio-thumb` photos with prev/next buttons, arrow
  keys, or Escape/backdrop-click to close. The lightbox JS reads the thumbnail list dynamically, so adding another
  `.portfolio-thumb` button automatically includes it in the slideshow — no JS changes needed for new photos.
- `pricing.html` — renamed from `quote.html` on 2026-09-07 at the user's request. Has a "Financing Available" box
  (no minimum project size; "certain individuals may qualify for 0% financing"; links out to the user's real
  financing partner, Enhancify, at `https://www.enhancify.com/fourth-light-farm-construction` — don't change that
  URL or invent different terms/partners without the user saying so) above the quote-request form. The form itself
  is unchanged: on submit it builds a `mailto:` link addressed to `fourthlightfarm@gmail.com` (pre-filled
  subject/body from the form fields) and navigates the browser there — it opens the visitor's own email app for them
  to hit send. There is no server-side form backend; nothing is silently submitted in the background. See Deployment
  below for why, and what an upgrade would require.
- `theme.css` — all custom styling, layered on top of the Bulma CSS framework (loaded from a CDN, not vendored).
- `logo.png` — the real FLFC logo (cow head + hand saw silhouette, recolored to `--flfc-earth-brown` with "FLFC LLC"
  text below it), generated 2026-08-21 from a source image the user supplied. Not a placeholder — don't regenerate or
  restyle it without the user asking.
- `CNAME` — contains `flfconstruction.com`. GitHub Pages custom domain file; only touch this if the user explicitly
  asks to change the site's domain.

Icons come from Font Awesome, loaded via CDN. There is no npm/node project here — don't add `package.json`, a
bundler, or a frontend framework unless the user explicitly asks for that kind of overhaul.

All three pages share the same nav bar and footer. When adding a nav item, page, or footer link, update it in
`index.html`, `portfolio.html`, and `pricing.html` together so they stay in sync — this bit them once already when
`mission.html` on the sister `flf` site drifted out of sync with `index.html`.

## Page structure

`index.html`:
- `#home` — hero section with logo, tagline, "Get Pricing" and "Our Services" buttons
- `#about` — About Us copy
- `#services` — four service cards (General Contracting, Custom Tile, Rot Repair, Architectural Drafting). Cards use
  `height: 100%` + flex column layout (see `theme.css` `.card` rules) so they stay equal height regardless of how
  much text is in each one — don't remove that when editing card content.
- `#impact` — "Building With a Purpose" box explaining the 10%-of-project-cost donation to Fourth Light Farm
- `#contact` — contact info
- `#game` — "Cow Catapult," a silly slingshot mini-game (drag the cow, launch it at the house) added 2026-08-30 at
  the user's request. Self-contained Canvas 2D game, no library, logic lives in the same inline `<script>` block at
  the bottom of `index.html` after the smooth-scroll code, styles under "Cow Catapult mini-game" in `theme.css`.
  Colors are pulled from the `--flfc-*` CSS variables at runtime so it stays in sync with the site palette. A direct
  hit spawns `debris`/`dustParticles` (small physics-driven rectangles + fading gray puffs) instead of just drawing
  the house — `houseDestroyed` flips to `true` and `drawHouse()` stops being called, so the settled debris pile
  doubles as the "wreckage." The hit message is a fixed string the user dictated verbatim — "UH OH TIME TO CALL FLFC!
  GET MOOVING!" — don't rewrite its wording/casing/punctuation without being asked. `resetGame()` clears `debris`,
  `dustParticles`, and `houseDestroyed` along with the cow. This is a fun easter egg, not a business-critical
  feature — treat requests to tweak it (power, house size, cow look) as low-risk/quick iterations, not something
  requiring the same caution as the quote form or contact info.
  Testing note: `requestAnimationFrame` does not fire at all in this project's dev sandbox/browser-preview tool (confirmed
  via a bare rAF counter test), so the animated flight/explosion can't be watched live there — verify game logic by
  temporarily exposing `{ update, draw, resetGame, getState, getCow }` on `window` right after `loop()` is called,
  driving frames by calling `update()` directly in a loop from the browser tool's JS-eval, then removing that debug
  hook before committing. Real browsers run rAF normally; this is purely a tooling limitation.

`portfolio.html` — page header, then a grid of project cards (see placeholders below), then a "Start Your Project"
CTA linking to `pricing.html`.

`pricing.html` — page header, then the "Financing Available" box, then the quote-request form (name, email, phone,
service dropdown, address, project details) with inline validation, plus a fallback line with the phone number and
email for people who'd rather not use the form.

When asked to add a new card, section, or nav item, follow the existing pattern (Bulma `columns`/`column`/`card`
classes) rather than introducing new layout systems.

## Known placeholders — flag these, don't silently invent real-looking values

- `portfolio.html` now has 4 real project photos (added 2026-08-21, all tagged "Custom Tile" — a tub surround, a
  pebble-floor walk-in shower, a frameless glass shower, and a marble-look bath remodel; files live in `images/`)
  plus one "More Projects Coming Soon" card. Don't invent project names/locations for the real photos beyond what's
  visibly true from the image, and don't invent fake completed projects for General Contracting, Rot Repair, or
  Architectural Drafting — those categories have no real photos yet, so leave the "coming soon" card as-is until the
  user supplies more.
- There is no license number displayed anywhere on the site — the user confirmed one isn't needed/applicable, so
  don't add one back in.

Do not remove the `#impact` section's link to fourthlightfarm.com without the user asking — it's the connection to
the affiliated nonprofit.

## Styling conventions

- All brand colors are CSS custom properties defined in `theme.css` under `:root` (e.g. `--flfc-medium-green`,
  `--flfc-earth-brown`, `--flfc-sage-green`). As of 2026-08-19 this deliberately matches the `flf` nonprofit site's
  palette exactly (same hex values, same sage-green/earth-brown/cream family) per the user's request to visually tie
  the two sites together — this is no longer a placeholder to be swapped out; treat it as the real brand palette
  unless the user says otherwise.
- Prefer Bulma utility classes already in use (`has-text-centered`, `is-fullwidth`, `section`, etc.) over new custom
  CSS when possible.
- The site must stay responsive — there's a mobile breakpoint block at the bottom of `theme.css` (`@media screen and
  (max-width: 768px)`). Check any layout change against narrow viewports.

## Deployment

**Live.** Hosted on GitHub Pages from `github.com/fourthlightfarm/flfconstruction`, serving the `main` branch root,
custom domain `flfconstruction.com` via the `CNAME` file and DNS A records pointed at GitHub Pages. Any commit
pushed to `main` goes live automatically within a few minutes — same model as the `flf` site.

- Don't push half-finished or obviously broken changes to `main`.
- Only commit and push when the user actually confirms they want the change live — don't push proactively mid-
  conversation.
- The `pricing.html` form uses `mailto:` rather than a real backend specifically because this is a static site with no
  server. If the user wants true silent/one-click submission (no email app popup for the visitor), that requires a
  third-party form service (e.g. Formspree, Web3Forms) that *the user* signs up for themselves — an agent should
  never create such an account on their behalf. Once they have an endpoint/key, wire the form's `action` to it and
  remove the `mailto:` JS.

## General approach

- Make the smallest edit that satisfies the request. This is a small business site, not a codebase that needs
  abstraction or refactors.
- After editing, describe the change in plain, non-technical language (what changed and where on the page).
- If a request is ambiguous, ask a clarifying question or make a reasonable interpretation and clearly say what you
  did, rather than guessing silently on something visual and hard to undo by eye.
- Never replace a bracketed placeholder with a plausible-looking but invented value (fake project history, fake
  license number, fake founding year, etc.) — leave it as a placeholder or ask the user for the real value.
