# Issue Tracker — Driver Insurance Hub (driverinsurancehub.com) — 2026-09-17

| # | Issue | Category | Severity | Effort | Fix Guide | Status |
|---|---|---|---|---|---|---|
| 1 | Cloudflare blocking Googlebot (403) — now GSC-confirmed | Crawlability | 🔴 Critical | Moderate | `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md` | ⬜ Not started |
| 2 | 450/654 pages not indexed (315 discovered-not-indexed, 72 crawled-not-indexed) | Indexability | 🔴 Critical | Major | `fixes/site-architecture/driverinsurancehub.com--orphan-pages-no-internal-links.md` | ⬜ Not started |
| 3 | 44 orphan pages (no incoming internal links) | Site Architecture | 🔴 Critical | Moderate | `fixes/site-architecture/driverinsurancehub.com--orphan-pages-no-internal-links.md` | ⬜ Not started |
| 4 | No meta description on 614/731 pages | Indexability | 🟠 High | Major (per-page) | `fixes/indexability/driverinsurancehub.com--missing-meta-descriptions.md` | ⬜ Not started |
| 5 | Title too long on 273/731 pages | Indexability | 🟠 High | Major (per-page) | `fixes/indexability/driverinsurancehub.com--overly-long-page-titles.md` | ⬜ Not started |
| 6 | No baseline security response headers | Security & International | 🟠 High | Quick win | `fixes/security-international/missing-security-headers.md` | ⬜ Not started (unverified this run) |
| 6b | No Yoast Focus Keyphrase on any of 543 pages/posts (100%) | Indexability | 🟠 High | Major (per-page) | `fixes/indexability/driverinsurancehub.com--no-focus-keyphrase-set.md` | ⬜ Not started |
| 7 | Duplicate google-site-verification tag | Indexability | 🟡 Medium | Quick win | `fixes/indexability/driverinsurancehub.com--duplicate-google-site-verification-tag.md` | ⬜ Not started |
| 8 | Site title wraps mid-word on mobile | Mobile | 🟡 Medium | Quick win | `fixes/mobile/driverinsurancehub.com--site-title-wrapping-mid-word.md` | ⬜ Not started (unverified this run) |
| 9 | Multiple H1 tags on 7 pages | Site Architecture | 🟡 Medium | Quick win | `fixes/site-architecture/multiple-h1-tags.md` | ⬜ Not started |
| 10 | No favicon | Site Architecture | 🟢 Low | Quick win | `fixes/site-architecture/driverinsurancehub.com--missing-favicon.md` | ⬜ Not started |
| 11 | No Article schema on state/city guides | Structured Data | 💡 Suggestion | Moderate | `fixes/structured-data/missing-schema-markup.md` | ⬜ Not started (unverified this run) |
| 12 | 115 redirects one click from homepage — needs a dedicated look | Crawlability | 💡 Suggestion | Moderate | — (not yet a fix guide; investigate first) | ⬜ Not started |

**Severity:** 🔴 Critical · 🟠 High · 🟡 Medium · 🟢 Low · 💡 Suggestion
**Effort:** Quick win (minutes) · Moderate (hours) · Major (dev project)
**Status:** ⬜ Not started · 🔧 In progress · ✅ Fixed & verified · ⏭️ Skipped (reason: ...)

**Recommended order of attack:** #1 and #3 first (both are quick-to-moderate effort and #3 is
likely the biggest lever on #2, the highest-impact issue on the site) → #2 will improve as #1 and
#3 land and Google re-crawls → #4 and #5 next (high-volume but mechanical, start with the highest
sampled-traffic pages per GSC Performance) → #6, #7, #9, #10 (all quick wins) → #8, #11 (re-verify
first) → #12 (needs investigation before it's actionable).
