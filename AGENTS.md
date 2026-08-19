# Agent instructions for this repo

This repo is the marketing website for Fourth Light Farm Construction, LLC (FLFC), a for-profit general
contracting/construction company. FLFC is affiliated by donation with Fourth Light Farm, a sustainable-agriculture
nonprofit (see the separate `flf` repo) — FLFC is its own business, not the nonprofit itself. The person requesting
changes is likely non-technical. Optimize for the smallest, safest edit that achieves what they asked for, and
explain what you changed in plain terms afterward.

## What this site is

Static HTML pages, mirroring the structure of the `flf` (Fourth Light Farm) site it was derived from. No framework,
no build step, no package manager, no dependencies to install.

- `index.html` — the entire site (all sections: home, about, services, community impact, contact) and a small inline
  `<script>` at the bottom for the mobile nav toggle and smooth scrolling.
- `theme.css` — all custom styling, layered on top of the Bulma CSS framework (loaded from a CDN, not vendored).
- `logo.svg` — a placeholder text-based logo. Replace with real FLFC branding when it exists.
- No `CNAME` yet — this site has no custom domain configured. Add one (containing just the domain name, e.g.
  `flfconstruction.com`) once FLFC has a domain, and set up GitHub Pages / DNS to match.

Icons come from Font Awesome, loaded via CDN. There is no npm/node project here — don't add `package.json`, a
bundler, or a frontend framework unless the user explicitly asks for that kind of overhaul.

## Page structure (`index.html`)

- `#home` — hero section with logo, tagline, "Request a Quote" and "Our Services" buttons
- `#about` — About Us copy
- `#services` — three placeholder service cards (General Contracting, Renovations & Remodeling, New Construction)
- `#impact` — "Building With a Purpose" box explaining the donation affiliation with Fourth Light Farm
- `#contact` — contact info and footer

When asked to add a new card, section, or nav item, follow the existing pattern (Bulma `columns`/`column`/`card`
classes) rather than introducing new layout systems.

## Known placeholders — flag these, don't silently invent real-looking values

Real business details (service area, services, phone, email, domain, tagline, donation terms) were filled in on
2026-08-19 and are no longer placeholders — see the content in `index.html` directly. What's still outstanding:

- The domain `flfconstruction.com` is named in the Contact section as "(coming soon)" but there is still no `CNAME`
  file, no GitHub remote, and no hosting set up — see Deployment below. Don't remove the "(coming soon)" qualifier
  or turn it into a link until the site is actually live there.
- `logo.svg` is a plain text placeholder, not a designed logo — replace when real branding exists.
- There is no quote-request form backend; the "Send Us a Message" button is a plain `mailto:` link. If the user
  wants an actual web form (unlike the `flf` site's newsletter, which posts to a Google Apps Script), that would
  need a backend added.

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

Not yet deployed. There is no GitHub remote, no GitHub Pages config, and no `CNAME` file. When the user is ready to
publish, set up a git repo, a GitHub remote, GitHub Pages (serving from `main:/`), and a `CNAME` file together —
don't add a `CNAME` speculatively before a domain is chosen.

## General approach

- Make the smallest edit that satisfies the request. This is a small business site, not a codebase that needs
  abstraction or refactors.
- After editing, describe the change in plain, non-technical language (what changed and where on the page).
- If a request is ambiguous, ask a clarifying question or make a reasonable interpretation and clearly say what you
  did, rather than guessing silently on something visual and hard to undo by eye.
- Never replace a bracketed placeholder with a plausible-looking but invented value (fake phone number, fake license
  number, fake founding year, etc.) — leave it as a placeholder or ask the user for the real value.
