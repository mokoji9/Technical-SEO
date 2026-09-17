# Changelog — AI Liability Guide (ailiabilityguide.com)

## 2026-09-06 — Initial audit

- Ran full automated technical SEO sweep (DataForSEO OnPage/Lighthouse, live browser rendering,
  curl UA/status checks, robots.txt/sitemap review).
- Findings written to `findings.md`, prioritized in `issue-tracker.md`.
- New fix guides added to the project's `fixes/` library:
  - `fixes/indexability/ailiabilityguide.com--overly-long-page-titles.md`
  - `fixes/site-architecture/ailiabilityguide.com--missing-favicon.md`
  - (reused existing `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`,
    `fixes/security-international/missing-security-headers.md`, and
    `fixes/structured-data/missing-schema-markup.md`)
- Published designed HTML report: `report.html` →
  https://claude.ai/code/artifact/fd51404e-2b17-4732-be69-b3c9e8cca9bb
- No fixes applied yet — all 6 issues are ⬜ Not started, pending the site owner's action
  (especially confirming the Cloudflare/crawl-access finding via Google Search Console before
  changing any Cloudflare settings).
