# Issue Tracker — Driver Insurance Hub (driverinsurancehub.com) — 2026-09-06

| # | Issue | Category | Severity | Effort | Fix Guide | Status |
|---|---|---|---|---|---|---|
| 1 | Cloudflare bot protection challenges/blocks non-browser crawl requests (confirmed 403 + noindex on spoofed Googlebot UA and on DataForSEO's Lighthouse crawler) | Crawlability | 🔴 Critical | Quick win | `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md` | ⬜ Not started |
| 2 | No meta description on any page checked (homepage + state page); og:description shows broken "[…]" truncation | Indexability | 🟠 High | Quick win | `fixes/indexability/driverinsurancehub.com--missing-meta-descriptions.md` | ⬜ Not started |
| 3 | No baseline security headers (HSTS, CSP, X-Frame-Options, X-Content-Type-Options, Referrer-Policy) | Security & International | 🟠 High | Quick win | `fixes/security-international/missing-security-headers.md` | ⬜ Not started |
| 4 | Site title wraps mid-word on mobile ("Driver / Insura / nce / Hub") due to overflow-wrap: anywhere on a too-narrow header column | Mobile | 🟡 Medium | Quick win | `fixes/mobile/driverinsurancehub.com--site-title-wrapping-mid-word.md` | ⬜ Not started |
| 5 | Duplicate google-site-verification meta tag | Indexability | 🟡 Medium | Quick win | `fixes/indexability/driverinsurancehub.com--duplicate-google-site-verification-tag.md` | ⬜ Not started |
| 6 | Page titles run past ~60 characters (72-75+ chars) across homepage and state pages | Indexability | 🟡 Medium | Moderate | `fixes/indexability/driverinsurancehub.com--overly-long-page-titles.md` | ⬜ Not started |
| 7 | No favicon site-wide | Site Architecture | 🟢 Low | Quick win | `fixes/site-architecture/driverinsurancehub.com--missing-favicon.md` | ⬜ Not started |
| 8 | No Article schema on ~50 state guide pages | Structured Data | 💡 Suggestion | Moderate | `fixes/structured-data/missing-schema-markup.md` | ⬜ Not started |

**Severity:** 🔴 Critical · 🟠 High · 🟡 Medium · 🟢 Low · 💡 Suggestion
**Effort:** Quick win (minutes) · Moderate (hours) · Major (dev project)
**Status:** ⬜ Not started · 🔧 In progress · ✅ Fixed & verified · ⏭️ Skipped (reason: ...)

## Recommended order of attack

1. **#1 first** — confirm via Google Search Console → URL Inspection → Test Live URL whether real
   Googlebot is actually affected, then fix the Cloudflare Bot Fight Mode / Verified Bots setting.
2. **#2 and #3** — both quick wins with sitewide impact: write real meta descriptions (starting
   with the homepage and highest-traffic states) and add security headers at the Cloudflare edge.
3. **#4** — fix the mobile header CSS; small, high-visibility bug affecting every mobile visit.
4. **#5 and #7** — trivial cleanups (duplicate tag removal, favicon upload), no reason to defer.
5. **#6** — rewrite titles; touches ~50 pages, worth batching with #2 since both live in the same
   Yoast snippet editor per page.
6. **#8** — Article schema rollout across state pages; worth doing once titles/descriptions are
   settled since it's templated the same way.
