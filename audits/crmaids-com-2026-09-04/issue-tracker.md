# Issue Tracker — crmaids.com — 2026-09-04

| # | Issue | Category | Severity | Effort | Fix Guide | Status |
|---|---|---|---|---|---|---|
| 1 | `page-sitemap1.xml` & `page-sitemap2.xml` time out / return 500 instead of XML | Crawlability | 🔴 Critical | Moderate (hosting/plugin config) | `fixes/crawlability/sitemap-file-timeout-error.md` | ⬜ Not started |
| 2 | Homepage is ~7.8-8.0MB; several uncompressed ~620-640KB JPEGs driving 5-6s LCP | Performance | 🟠 High | Moderate | `fixes/performance/unoptimized-images.md` | ⬜ Not started |
| 3 | 8 render-blocking resources on homepage | Performance | 🟠 High | Moderate | `fixes/performance/render-blocking-resources.md` | ⬜ Not started |
| 4 | Cumulative Layout Shift 0.178 (needs improvement) | Performance | 🟡 Medium | Moderate (follows from #2) | `fixes/performance/unoptimized-images.md` | ⬜ Not started |
| 5 | Viewport meta disables pinch-zoom (`user-scalable=0`) | Mobile | 🟡 Medium | Quick win | `fixes/mobile/missing-viewport-meta.md` | ⬜ Not started |
| 6 | `robots.txt` has redundant/stale rule blocks from a non-WordPress structure | Crawlability | 🟢 Low | Quick win | `fixes/crawlability/robots-txt-blocking-pages.md` | ⬜ Not started |
| 7 | `/contact` 301s to `/contact/` (internal links should use canonical form) | Site architecture | 🟢 Low | Quick win | *(update internal links directly; no dedicated guide needed)* | ⬜ Not started |
| 8 | 3 duplicate `<meta name="generator">` tags + duplicate `ti-site-data` tag | Indexability | 🟢 Low | Quick win | *(cosmetic HTML cleanup; no dedicated guide needed)* | ⬜ Not started |
| 9 | No `LocalBusiness`/`Organization` schema on homepage | Structured data | 💡 Suggestion | Moderate | `fixes/structured-data/missing-schema-markup.md` | ⬜ Not started |
| 10 | Heavy third-party script footprint (GTM, Meta Pixel, Bing UET, Ads, Clarity, Elfsight, GoHighLevel, UserWay) | Performance | 💡 Suggestion | Moderate | *(audit + defer non-critical scripts; see Suggestions in findings.md)* | ⬜ Not started |

**Severity:** 🔴 Critical · 🟠 High · 🟡 Medium · 🟢 Low · 💡 Suggestion
**Effort:** Quick win (minutes) · Moderate (hours) · Major (dev project)
**Status:** ⬜ Not started · 🔧 In progress · ✅ Fixed & verified · ⏭️ Skipped (reason: ...)

## Recommended order of attack

1. **#1 first** — this is the one confirmed, critical bug, reproduced identically across two
   full audit passes today. Get your host to check the server error log for the exact timeout
   cause on `page-sitemap1.xml`/`page-sitemap2.xml`, since these are the sitemaps most likely
   covering your core service/location pages. Verify the fix in Google Search Console →
   Sitemaps afterward.
2. **#2 and #3 together** — compress/convert the handful of oversized JPEGs to WebP and add
   explicit width/height, then address render-blocking scripts. These two together should move
   the Performance score meaningfully and also improve #4 (CLS) as a side effect.
3. **#5** — quick one-line fix to the viewport tag, immediate accessibility/mobile-usability win.
4. **#6, #7, #8** — batch these as a single low-effort cleanup pass; none are urgent individually.
5. **#9** — schema expansion for local-pack visibility; good ROI for a local service business,
   not urgent.
6. **#10** — third-party script audit; fold into the performance work in #2/#3 rather than doing
   separately.
