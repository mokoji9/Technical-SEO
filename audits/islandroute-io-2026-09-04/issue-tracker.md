# Issue Tracker — islandroute.io — 2026-09-04

| # | Issue | Category | Severity | Effort | Fix Guide | Status |
|---|---|---|---|---|---|---|
| 1 | Cloudflare bot protection may be blocking/challenging search crawlers | Crawlability | 🔴 Critical | Quick win (config change) | `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md` | ⬜ Not started |
| 2 | 51 of 54 homepage images missing `alt` text | On-page content | 🟠 High | Moderate | *(no guide yet — see suggestion to add On-Page Content checklist)* | ⬜ Not started |
| 3 | `/old-home` is thin placeholder content, live in sitemap.xml | Indexability / Site architecture | 🟡 Medium | Quick win | *(use `fixes/indexability/accidental-noindex.md` pattern in reverse, or redirect — needs a dedicated "thin content" guide)* | ⬜ Not started |
| 4 | Only `WebSite` schema present — no Organization/FAQPage schema | Structured data | 🟡 Medium | Moderate | `fixes/structured-data/missing-schema-markup.md` | ⬜ Not started |
| 5 | All sitemap.xml `lastmod` dates identical/static | Crawlability | 🟢 Low | Moderate (dev fix to sitemap generation) | *(no guide yet)* | ⬜ Not started |
| 6 | Lighthouse "Agentic Browsing" score 50/100 | Suggestion | 💡 Suggestion | — | — | ⬜ Not started |

**Severity:** 🔴 Critical · 🟠 High · 🟡 Medium · 🟢 Low · 💡 Suggestion
**Effort:** Quick win (minutes) · Moderate (hours) · Major (dev project)
**Status:** ⬜ Not started · 🔧 In progress · ✅ Fixed & verified · ⏭️ Skipped (reason: ...)

## Recommended order of attack

1. **#1 first** — verify via Google Search Console URL Inspection, then fix Cloudflare
   settings. This is the one issue that could be silently tanking indexing entirely; everything
   else is secondary until this is confirmed clean.
2. **#2** — alt text audit, straightforward content fix, improves both accessibility and image
   search visibility.
3. **#3** — decide whether `/old-home` should redirect, noindex, or be removed from the
   sitemap — needs a quick decision from whoever owns the site content.
4. **#4** — schema expansion, good ROI for a travel app (FAQ rich results especially).
5. **#5** — low priority, fold into a future dev sprint if the sitemap is auto-generated.
