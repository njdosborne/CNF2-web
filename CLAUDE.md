# CNF2-web - Claude Project Memory

Working repo for **curenf2.org** (Cure NF2 charity site, WordPress.com-hosted), an
AcmeCloud spoke. No Azure/Terraform footprint: the site is SaaS-hosted, so the
integration surface is MCP + WordPress Studio, and this repo is the review gate.

## The two MCPs - keep them straight

- **`wordpress-studio`** (local): the sandbox. Day-to-day dev happens here -
  file edits, WP-CLI, screenshots. Zero risk to the live site.
- **`wpcom-mcp`** (live): production curenf2.org. Read freely. Writes are
  **draft-only**: never set `status: publish` and never touch the site facade
  (settings, themes, plugins) without Neil's explicit go-ahead in the moment.
  A standing instruction to "work on the site" is not publish approval.

## Review-before-publish - NON-NEGOTIABLE

Every change ships through review, in both directions (Neil reviews Claude's
work, Claude reviews Neil's):

1. Edit the **local Studio copy** first, commit to this repo.
2. Review = git diff here, plus `studio preview create` / `studio preview
   update` for a shareable visual (`wp.build` URL, public, expires 7 days after
   last update - nothing sensitive goes on a preview).
3. Deploy only after approval:
   - Code/theme/files: **selective Studio Sync push**. Never push the database
     to live - a DB push replaces the entire live database.
   - Content: create as **draft** on live via `wpcom-mcp`, publish after review.

## Site copy rules

- Plain ASCII punctuation in all shipped copy (no em/en dashes, no ellipsis).
- No fabricated content presented as real: no invented testimonials, stats,
  research claims, or events. This is a medical charity site - factual claims
  about NF2 (neurofibromatosis type 2) must come from Neil or cited sources.
- Judge features by "usable by a 2-person charity".

## Local paths

- Studio site copy: `C:\Users\njdos\Studio\<site>` (set once Studio is
  installed and the site is pulled; update this line when known).
- Studio auth and WordPress.com MCP OAuth are Neil's browser steps; if a tool
  fails auth, ask rather than working around it.
