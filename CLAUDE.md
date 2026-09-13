# CNF2-web - Claude Project Memory

Working repo for **curenf2.org** (Cure NF2 charity site, WordPress.com-hosted), an
AcmeCloud spoke. No Azure/Terraform footprint: the site is SaaS-hosted, so the
integration surface is MCP + WordPress Studio, and this repo is the review gate.

## Sites and IDs (WordPress.com, via `wpcom-mcp`)

| Environment | Site ID | URL | Rule |
|---|---|---|---|
| Production | 147892643 | https://curenf2.org | Read freely. Writes draft-only, never `status: publish`, never the site facade (settings/themes/plugins) without Neil's go-ahead in the moment. |
| Staging (UAT) | 253312726 | https://staging-e99b-nf2biosolutions.wpcomstaging.com | The assistant's write target. Still requires the MCP `user_confirmed` flow. |

- A standing instruction to "work on the site" is not publish approval.
- Business plan, owned by Nicole Henwood's account (`nf2bio`); Neil's account
  `njdof57b43397e9` is an administrator on both sites (added to staging
  2026-09-09). Site-level MCP toggle lives in Hosting Dashboard > Settings > AI tools.
- Staging is a SNAPSHOT, not a mirror. Before starting work: Hosting Dashboard >
  staging > Sync > Pull from Production (files + database). Promotion is
  Push to Production: files selectively; database push replaces the whole live
  DB, so only push DB when staging was the sole place edited since the pull.
- Pre-rebrand site archive (the staging content as of 2026-03-11, old "NF2
  BioSolutions" branding): `c:\project\CNF2-old-site-mirror` (wget mirror +
  `_content-export/*.json` from the REST API + index.html). Not in git. A
  6 GB Jetpack backup of the same staging site also exists in WordPress.com.

## Optional local sandbox (`wordpress-studio`)

WordPress Studio on the laptop, for deeper theme work. Not installed yet.
Its MCP (`studio mcp`) drives the local copy; Studio Sync pulls/pushes to
WordPress.com. Same review rules apply.

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
