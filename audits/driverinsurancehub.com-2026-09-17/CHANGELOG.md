# Changelog — Driver Insurance Hub (driverinsurancehub.com)

## 2026-09-17

- Ran a follow-up automated audit, this time including a direct connected-account check via
  Claude in Chrome (Google Search Console + Ahrefs Site Audit), per the updated
  technical-seo-audit workflow.
- **Confirmed** the 2026-09-06 Cloudflare-blocking finding with real GSC data (50 pages blocked
  403) — previously only confirmed via a spoofed user-agent test.
- **Confirmed at full-site scale** (via Ahrefs) two issues previously only sampled on 2 pages:
  missing meta descriptions (614/731 pages) and overly-long titles (273/731 pages, upgraded to
  High severity given the scale).
- **New finding:** only 204/654 known pages (31%) are indexed by Google; 387 of the 450
  not-indexed pages are "discovered" or "crawled" but not prioritized for indexing — not blocked
  by anything specific.
- **New finding:** 44 orphan pages with no incoming internal links (Ahrefs Site Audit) — the
  likely structural root cause of a large share of the indexing gap above. New fix guide written:
  `fixes/site-architecture/driverinsurancehub.com--orphan-pages-no-internal-links.md`.
- **New finding:** 7 pages with multiple `<h1>` tags (Ahrefs Site Audit); references the existing
  generic `fixes/site-architecture/multiple-h1-tags.md` guide.
- **New finding:** checked the WordPress admin directly and found all 543 published pages/posts
  (94 pages + 449 posts, 100%) have no Yoast Focus Keyphrase set — the likely process root cause
  behind the sitewide meta-description and title-length gaps, since Yoast's on-page checklist
  never actually triggers without one. New fix guide:
  `fixes/indexability/driverinsurancehub.com--no-focus-keyphrase-set.md`.
- **Corrected a defect in the 2026-09-06 audit's delivered materials**: two of its linked fix
  guides (`overly-long-page-titles.md`, `missing-favicon.md`) were actually written for a
  different site (ailiabilityguide.com) that happened to hit the same generic issue name first.
  Split into site-scoped guides (`driverinsurancehub.com--overly-long-page-titles.md`,
  `driverinsurancehub.com--missing-favicon.md`) with this site's real content and drafted
  rewrites; repointed all references in the 2026-09-06 audit's own `findings.md`,
  `issue-tracker.md`, `report.html`, and `CHANGELOG.md`. Also site-scoped three other
  driverinsurancehub-only guides (`missing-meta-descriptions.md`,
  `duplicate-google-site-verification-tag.md`, `site-title-wrapping-mid-word.md`) to prevent the
  same collision going forward.
- Not independently re-verified this run (carried forward from 2026-09-06 as still-open):
  security response headers, mobile title-wrap bug, Article schema on state pages.

## 2026-09-06

See `../driverinsurancehub.com-2026-09-06/CHANGELOG.md` for the original audit's log.
