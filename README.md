# Fourth Light Farm Construction, LLC — Website

The website for Fourth Light Farm Construction, LLC (FLFC), a general contracting and construction company
affiliated by donation with [Fourth Light Farm](https://fourthlightfarm.com), a sustainable-agriculture nonprofit.

It's a simple, static website — just HTML and CSS, no build step, no server — scaffolded from the structure of the
Fourth Light Farm nonprofit site. That makes it easy to edit, including with an AI coding agent, even if you don't
know how to code.

**This site is still a work in progress.** Most business details are filled in now (phone, email, service area,
services, domain name, tagline), but the license number, a real logo, and hosting are still placeholders — see
`AGENTS.md` for the full list. Fill those in (or ask an AI agent to help you fill them in) before treating the site
as ready to publish.

## Making changes with an AI agent (no coding experience needed)

You can update this site by describing what you want in plain English to [Claude Code](https://claude.com/claude-code)
(or a similar AI coding assistant) and letting it make the edit for you.

1. **Open Claude Code in this project folder.** If you don't have it installed, see https://claude.com/claude-code
   for setup instructions. Once installed, open a terminal, navigate to this folder, and run `claude`.
2. **Say what you want changed, in plain language.** For example:
   - "Our phone number is 603-555-0199, add it to the Contact section and footer."
   - "We do roofing and siding too, add those as service cards."
   - "Change the accent color from amber to a deep red."
3. **Review what it changed.** Claude Code will show you a diff (a before/after) of the file(s) it edited. You don't
   need to understand code — just read the section it changed and check that it looks right.
4. **Once you're ready to go live**, ask the agent to help set up a git repository, a GitHub remote, and GitHub Pages
   — none of that exists yet for this site.

The file [`AGENTS.md`](./AGENTS.md) in this repo has more details for the agent about how this site is put together
and the placeholders that still need real values. You don't need to read it yourself — the agent will use it
automatically.

## What's in this repo

- `index.html` — the entire site (home, about, services, community impact, contact)
- `theme.css` — colors, fonts, and styling (placeholder palette — not final brand colors)
- `logo.svg` — a placeholder text-based logo (not a designed logo)

## Previewing locally

No build step or install is required. Just open `index.html` in a browser, or serve the folder locally:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deployment

Not deployed yet. This repo has no git history and no GitHub remote — it was scaffolded from the structure of the
`flf` (Fourth Light Farm nonprofit) site as a starting point. Once the business details are filled in and you're
ready to publish, set up a git repo, a GitHub remote, and GitHub Pages (or another static host) to go live.
