# Issue Tracker — AI Liability Guide (ailiabilityguide.com) — 2026-09-06

| # | Issue | Category | Severity | Effort | Fix Guide | Status |
|---|---|---|---|---|---|---|
| 1 | Cloudflare bot protection challenges/blocks non-browser crawl requests (confirmed 403 + noindex on spoofed Googlebot UA and on DataForSEO's Lighthouse crawler) | Crawlability | 🔴 Critical | Quick win | `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md` | ⬜ Not started |
| 2 | No baseline security headers (HSTS, CSP, X-Frame-Options, X-Content-Type-Options, Referrer-Policy) | Security & International | 🟠 High | Quick win | `fixes/security-international/missing-security-headers.md` | ⬜ Not started |
| 3 | FAQ content on pillar pages not marked up as FAQPage schema | Structured Data | 🟡 Medium | Quick win | `fixes/structured-data/missing-schema-markup.md` | ⬜ Not started |
| 4 | Page titles run past ~60 characters (e.g. 95 chars on /ai-liability/) | Indexability | 🟡 Medium | Moderate | `fixes/indexability/ailiabilityguide.com--overly-long-page-titles.md` | ⬜ Not started |
| 5 | No favicon site-wide | Site Architecture | 🟢 Low | Quick win | `fixes/site-architecture/ailiabilityguide.com--missing-favicon.md` | ⬜ Not started |
| 6 | Content reads at very high complexity/negative-readability level sitewide | Content quality (suggestion) | 💡 Suggestion | Major | — (editorial decision, no technical fix) | ⬜ Not started |

**Severity:** 🔴 Critical · 🟠 High · 🟡 Medium · 🟢 Low · 💡 Suggestion
**Effort:** Quick win (minutes) · Moderate (hours) · Major (dev project)
**Status:** ⬜ Not started · 🔧 In progress · ✅ Fixed & verified · ⏭️ Skipped (reason: ...)

## Recommended order of attack

1. **#1 first** — confirm via Google Search Console → URL Inspection → Test Live URL whether
   real Googlebot is affected, then fix the Cloudflare Bot Fight Mode / Verified Bots setting.
   Highest possible impact (site could be silently losing crawl coverage) for minimal effort.
2. **#2 next** — add security headers at the Cloudflare edge (Transform Rules), a few minutes
   of work, no code deploy needed.
3. **#3** — add FAQPage schema to the pillar pages that already have FAQ sections; content is
   already written, this is just markup.
4. **#5** — add a favicon via WordPress Site Identity settings; trivial, no reason to defer.
5. **#4** — rewrite titles page-by-page (or adjust the Yoast title template) since it touches
   more pages and is worth doing carefully rather than quickly.
6. **#6** — a longer-term editorial conversation, not a sprint item.
