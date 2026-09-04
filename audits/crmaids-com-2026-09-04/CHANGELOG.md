# Changelog — crmaids.com

## 2026-09-04

- Automated audit run (requested twice the same day). Both passes produced identical results:
  `page-sitemap1.xml` and `page-sitemap2.xml` time out with `Status: 000` after 30s on every
  attempt (5 attempts total across both passes, curl + real browser + Googlebot UA), robots.txt
  unchanged, viewport tag still disables pinch-zoom, structured data types unchanged, duplicate
  generator tags unchanged. Lighthouse scores moved only within normal run-to-run noise
  (Performance 0.54-0.56, LCP 5.1-6.0s, byte weight 7.8-8.0MB) — not a real change.
  Findings logged in `findings.md`, prioritized in `issue-tracker.md`. No fixes applied yet —
  all issues are `⬜ Not started`.
- Designed HTML client report produced (`report.html`, published as a Claude Artifact) from
  the findings above, using the site's real logo and brand blue. While preparing it the
  `page-sitemap1.xml` timeout was re-checked and reproduced again (HTTP 000, 0 bytes, 25s),
  while `post-sitemap1.xml` returned 200 in 1.4s. Still no fixes applied.
