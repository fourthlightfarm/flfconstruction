# Fourth Light Farm Construction, LLC — Website

The website for Fourth Light Farm Construction, LLC (FLFC), a general contracting and construction company
affiliated by donation with [Fourth Light Farm](https://fourthlightfarm.com), a sustainable-agriculture nonprofit.

It's a simple, static website — just HTML and CSS, no build step, no server — scaffolded from the structure of the
Fourth Light Farm nonprofit site. That makes it easy to edit, including with an AI coding agent, even if you don't
know how to code.

**Live at [flfconstruction.com](https://flfconstruction.com).** Business details (phone, email, service area,
services, tagline) are filled in. What's still a placeholder: the real logo (`logo.svg` is plain text for now) and
the six sample projects on `portfolio.html`, which need real photos and descriptions swapped in.

## Making changes with an AI agent (no coding experience needed)

You can update this site by describing what you want in plain English to [Claude Code](https://claude.com/claude-code)
(or a similar AI coding assistant) and letting it make the edit for you.

1. **Open Claude Code in this project folder.** If you don't have it installed, see https://claude.com/claude-code
   for setup instructions. Once installed, open a terminal, navigate to this folder, and run `claude`.
2. **Say what you want changed, in plain language.** For example:
   - "Add this project to the portfolio page: [details]."
   - "We do roofing and siding too, add those as service cards."
   - "Change the accent color from amber to a deep red."
3. **Review what it changed.** Claude Code will show you a diff (a before/after) of the file(s) it edited. You don't
   need to understand code — just read the section it changed and check that it looks right.
4. **Ask it to commit and push** when you want the change to go live. Once pushed to the `main` branch on GitHub,
   flfconstruction.com updates automatically within a few minutes.

The file [`AGENTS.md`](./AGENTS.md) in this repo has more details for the agent about how this site is put together
and the placeholders that still need real values. You don't need to read it yourself — the agent will use it
automatically.

## What's in this repo

- `index.html` — the main page (home, about, services, community impact, contact)
- `portfolio.html` — a gallery of past projects (currently placeholder content)
- `quote.html` — a "Request a Quote" form that opens the visitor's email app, pre-addressed to
  fourthlightfarm@gmail.com, with their project details filled in
- `theme.css` — colors, fonts, and styling (placeholder palette — not final brand colors)
- `logo.svg` — a placeholder text-based logo (not a designed logo)
- `CNAME` — the custom domain configuration (flfconstruction.com)

## Previewing locally

No build step or install is required. Just open `index.html` in a browser, or serve the folder locally:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deployment

This site is hosted on GitHub Pages directly from the `main` branch of
[github.com/fourthlightfarm/flfconstruction](https://github.com/fourthlightfarm/flfconstruction). Any change pushed
to `main` goes live automatically — there is no build or CI step in between.
