# Issue Tracker — AI Liability Guide (ailiabilityguide.com) — 2026-09-17

| # | Issue | Category | Severity | Effort | Fix Guide | Status |
|---|---|---|---|---|---|---|
| 1 | Cloudflare blocking Googlebot (403) — GSC-confirmed, now also breaking real page resources | Crawlability | 🔴 Critical | Moderate | `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md` | ⬜ Not started |
| 2 | 193/207 pages not indexed (151 discovered-not-indexed, 20 crawled-not-indexed) | Indexability | 🔴 Critical | Major | `fixes/site-architecture/ailiabilityguide.com--weak-internal-linking.md` | ⬜ Not started |
| 3 | 16 pages with only one incoming internal link; crawl hits max depth | Site Architecture | 🔴 Critical | Moderate | `fixes/site-architecture/ailiabilityguide.com--weak-internal-linking.md` | ⬜ Not started |
| 4 | 39 pages missing meta description, 2 too long | Indexability | 🟠 High | Major (per-page) | `fixes/indexability/ailiabilityguide.com--missing-meta-descriptions.md` | ⬜ Not started |
| 5 | Title too long on 96/351 pages | Indexability | 🟠 High | Major (per-page) | `fixes/indexability/ailiabilityguide.com--overly-long-page-titles.md` | ⬜ Not started |
| 6 | No Yoast Focus Keyphrase on any of 184 pages/posts (100%) | Indexability | 🟠 High | Major (per-page) | `fixes/indexability/ailiabilityguide.com--no-focus-keyphrase-set.md` | ⬜ Not started |
| 7 | No baseline security response headers | Security & International | 🟠 High | Quick win | `fixes/security-international/missing-security-headers.md` | ⬜ Not started (unverified this run) |
| 8 | FAQ content not marked up as FAQPage schema | Structured Data | 🟡 Medium | Quick win | `fixes/structured-data/missing-schema-markup.md` | ⬜ Not started (unverified this run) |
| 9 | Open Graph tags incomplete (207 pages) / OG URL mismatched canonical (12) | Structured Data | 🟡 Medium | Moderate | — (new, no guide yet) | ⬜ Not started |
| 10 | Minor link/status issues (broken links, 404/4xx, redirects) | Site Architecture | 🟡 Medium | Quick win | `fixes/site-architecture/broken-internal-links.md` | ⬜ Not started |
| 11 | No favicon | Site Architecture | 🟢 Low | Quick win | `fixes/site-architecture/ailiabilityguide.com--missing-favicon.md` | ⬜ Not started |
| 12 | Content reads at very high complexity level | Content quality (suggestion) | 💡 Suggestion | Major | — (editorial decision) | ⬜ Not started |
| 13 | GSC vs. Ahrefs noindex-count discrepancy (4 vs 16) worth a quick look | Indexability | 💡 Suggestion | Quick win | — (investigate first) | ⬜ Not started |

**Severity:** 🔴 Critical · 🟠 High · 🟡 Medium · 🟢 Low · 💡 Suggestion
**Effort:** Quick win (minutes) · Moderate (hours) · Major (dev project)
**Status:** ⬜ Not started · 🔧 In progress · ✅ Fixed & verified · ⏭️ Skipped (reason: ...)

**Recommended order of attack:** #1 first (fix the Cloudflare rule — it's both blocking crawl
access and actively breaking page resources) → #3 next (link in the 16 weakly-linked pages,
likely the biggest lever on #2) → let Google re-crawl and re-check the GSC indexing breakdown →
#4, #5, #6 together per page (meta description + title + focus keyphrase in one editing pass is
more efficient than three separate passes through the same content) → #7 (quick win, no code
deploy) → #8, #9, #10, #11 (all quick-to-moderate cleanups) → #12, #13 (editorial call / quick
investigation, lower urgency).
