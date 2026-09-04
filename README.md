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
| `templates/` | Blank templates for audit reports, issue tracking, and new fix guides. |

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

## Status

🟡 **Workflow setup in progress.** Repo structure and starter fix guides are being drafted.
Not yet connected to GitHub — say the word when you're ready to push this to a repository.
