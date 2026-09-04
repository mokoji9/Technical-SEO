# Technical SEO Hub

A reusable, beginner-friendly toolkit for finding and fixing technical SEO issues on any website.

This is **not** tied to one website. It's a framework you reuse every time you (or a client)
need a technical SEO audit:

1. Run an audit on a site → findings get logged in `/audits/{site-name}-{date}/`
2. Each finding is matched to a category in `/checklists/`
3. Each finding is matched to a step-by-step fix guide in `/fixes/`
4. Fixes get verified and logged in that audit's `CHANGELOG.md`

## Folder guide

| Folder | Purpose |
|---|---|
| `checklists/` | What to check, organized by category. Use these to scope an audit. |
| `fixes/` | Beginner-friendly, step-by-step guides for fixing each specific issue. |
| `audits/` | One folder per site per audit date. Contains the findings + prioritized issue list for that run. |
| `templates/` | Blank templates for audit reports, issue tracking, new fix guides, and a designed HTML client report (`report-template.html`). |

## The golden rule for every audit

**Before starting any audit, I will always ask you:**
> "Do you want this audit automated (using connected SEO tools) or do you want to provide the data manually (e.g. a Screaming Frog export, Search Console export, PageSpeed report)?"

This is a standing rule — never skip asking, even on repeat audits of the same site.

- **Automated** → uses connected tools (Semrush, DataForSEO, site crawlers, PageSpeed data, etc.)
- **Manual** → you paste in / upload data and I analyze it

See [`WORKFLOW.md`](WORKFLOW.md) for the full step-by-step process.

## Categories covered

- Crawlability (robots.txt, sitemap, crawl budget)
- Indexability (canonicals, noindex, duplicate content)
- Site architecture (URLs, internal linking, pagination)
- Performance (Core Web Vitals, page speed, TTFB)
- Mobile-friendliness
- Structured data (schema markup)
- Security & internationalization (HTTPS, status codes, hreflang)

## Also available as a Skill

This entire workflow is also packaged as a standalone Claude Skill (`technical-seo-audit`) —
self-contained, works in any project without this repo being cloned. Install it once
(`~/.claude/skills/technical-seo-audit/`) and it triggers automatically whenever you ask Claude
to check a site for SEO issues. Its bundled checklists/fixes/templates are copies of the ones
in this repo — when you add or edit any of those here, re-sync them into the skill's
`references/` folder to keep both in sync.

## Status

🟢 **Live.** Pushed to GitHub. First audit (islandroute.io) complete, including a designed
HTML report.
