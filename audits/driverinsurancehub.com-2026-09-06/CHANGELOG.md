# Changelog — Driver Insurance Hub (driverinsurancehub.com)

## 2026-09-06 — Initial audit

- Ran full automated technical SEO sweep (DataForSEO OnPage/Lighthouse, live browser rendering
  incl. mobile viewport, curl UA/status checks, robots.txt/sitemap review).
- Findings written to `findings.md`, prioritized in `issue-tracker.md`.
- New fix guides added to the project's `fixes/` library:
  - `fixes/indexability/driverinsurancehub.com--missing-meta-descriptions.md`
  - `fixes/mobile/driverinsurancehub.com--site-title-wrapping-mid-word.md`
  - `fixes/indexability/driverinsurancehub.com--duplicate-google-site-verification-tag.md`
  - (reused existing `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`,
    `fixes/security-international/missing-security-headers.md`,
    `fixes/indexability/driverinsurancehub.com--overly-long-page-titles.md`,
    `fixes/site-architecture/driverinsurancehub.com--missing-favicon.md`, and
    `fixes/structured-data/missing-schema-markup.md`)
- Published designed HTML report: `report.html` →
  https://claude.ai/code/artifact/425e3ec7-c433-4d3e-9ea3-c6728d70c88c
- No fixes applied yet — all 8 issues are ⬜ Not started, pending the site owner's action
  (especially confirming the Cloudflare/crawl-access finding via Google Search Console before
  changing any Cloudflare settings).
