# CNF2-web

Source and workflow repo for [curenf2.org](https://curenf2.org), the Cure NF2 site hosted on WordPress.com, developed under the AcmeCloud umbrella.

## How this repo is used

The live site is SaaS-hosted on WordPress.com, so there is no server infrastructure here. This repo versions the site's editable surface (theme, custom blocks, config, content exports) so that every change is reviewable as a git diff before it reaches the live site.

## Workflow

1. **Local sandbox**: the site is pulled into a local copy with [WordPress Studio](https://developer.wordpress.com/studio/) (free, runs on the laptop). Edits happen there first: theme files, CSS, blocks, content.
2. **Review**: changes are committed here and reviewed as diffs. For visual review, `studio preview create` publishes the local copy to a temporary public `wp.build` URL that anyone can open (expires 7 days after last update).
3. **Deploy**: approved changes go live via selective Studio Sync push (files and themes; never a database push to live) or, for content, via the WordPress.com MCP as drafts that are published after approval.

## Tooling

| Surface | Tool |
|---|---|
| Local sandbox | WordPress Studio + its MCP server (`studio mcp`) |
| Live site | WordPress.com MCP (`wpcom-mcp`) - write tools create drafts by default |
| Review | git diffs in this repo + Studio preview links |

See CLAUDE.md for the rules Claude Code sessions follow when working on this site.
