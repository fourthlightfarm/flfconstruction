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
- `portfolio.html` — a gallery page of past projects. **All six project cards are placeholders** (`[Project Name]`,
  "Project photo coming soon", generic placeholder description) — see the Known placeholders section below.
- `quote.html` — a quote-request form page. On submit it builds a `mailto:` link addressed to
  `fourthlightfarm@gmail.com` (pre-filled subject/body from the form fields) and navigates the browser there — it
  opens the visitor's own email app for them to hit send. There is no server-side form backend; nothing is silently
  submitted in the background. See Deployment below for why, and what an upgrade would require.
- `theme.css` — all custom styling, layered on top of the Bulma CSS framework (loaded from a CDN, not vendored).
- `logo.svg` — a placeholder text-based logo. Replace with real FLFC branding when it exists.
- `CNAME` — contains `flfconstruction.com`. GitHub Pages custom domain file; only touch this if the user explicitly
  asks to change the site's domain.

Icons come from Font Awesome, loaded via CDN. There is no npm/node project here — don't add `package.json`, a
bundler, or a frontend framework unless the user explicitly asks for that kind of overhaul.

All three pages share the same nav bar and footer. When adding a nav item, page, or footer link, update it in
`index.html`, `portfolio.html`, and `quote.html` together so they stay in sync — this bit them once already when
`mission.html` on the sister `flf` site drifted out of sync with `index.html`.

## Page structure

`index.html`:
- `#home` — hero section with logo, tagline, "Request a Quote" and "Our Services" buttons
- `#about` — About Us copy
- `#services` — four service cards (General Contracting, Custom Tile, Rot Repair, Architectural Drafting). Cards use
  `height: 100%` + flex column layout (see `theme.css` `.card` rules) so they stay equal height regardless of how
  much text is in each one — don't remove that when editing card content.
- `#impact` — "Building With a Purpose" box explaining the 10%-of-project-cost donation to Fourth Light Farm
- `#contact` — contact info and footer

`portfolio.html` — page header, then a grid of project cards (see placeholders below), then a "Start Your Project"
CTA linking to `quote.html`.

`quote.html` — a single quote-request form (name, email, phone, service dropdown, address, project details) with
inline validation, plus a fallback line with the phone number and email for people who'd rather not use the form.

When asked to add a new card, section, or nav item, follow the existing pattern (Bulma `columns`/`column`/`card`
classes) rather than introducing new layout systems.

## Known placeholders — flag these, don't silently invent real-looking values

- All six portfolio cards in `portfolio.html` (`[Project Name]` + placeholder description) are examples of the
  layout, not real completed jobs. Don't invent project names, locations, or details to fill them in — ask the user
  for real past projects (and real photos, to replace the "Project photo coming soon" boxes) instead.
- `logo.svg` is a plain text placeholder, not a designed logo — replace when real branding exists.
- There is no license number displayed anywhere on the site — the user confirmed one isn't needed/applicable, so
  don't add one back in.

Do not remove the `#impact` section's link to fourthlightfarm.com without the user asking — it's the connection to
the affiliated nonprofit.

## Styling conventions

- All brand colors are CSS custom properties defined in `theme.css` under `:root` (e.g. `--flfc-steel-blue`,
  `--flfc-charcoal`, `--flfc-amber`). This is a placeholder palette (steel blue/charcoal/amber) chosen to be distinct
  from the FLF nonprofit's sage-green farm palette — swap it out entirely once FLFC has real brand colors, rather
  than treating it as final.
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
- The `quote.html` form uses `mailto:` rather than a real backend specifically because this is a static site with no
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
