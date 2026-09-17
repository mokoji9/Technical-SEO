# Changelog — AI Liability Guide (ailiabilityguide.com)

## 2026-09-17 (re-verification pass, later same day)

- At the user's request, re-ran every check in this audit independently from scratch rather than
  reusing the earlier run's results. No fixes had been applied yet, so no finding changed status.
- Re-confirmed live: curl/UA checks, DataForSEO Lighthouse and on-page data (Best Practices still
  77), and WordPress's "No Focus Keyphrase" filter (still 18/18 pages) — all unchanged from the
  earlier run today.
- GSC and Ahrefs both still show the same "last update" timestamp as the earlier run (their own
  data-refresh lag) — those specific numbers are identical by definition, not skipped.
- **Refinement:** repeated curl checks a few seconds apart returned a mix of `200` and `403` for
  the same request — the Cloudflare block is intermittent/probabilistic, not a hard 100% block.
  Added this to the shared `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`
  guide since it applies beyond this one site.

## 2026-09-17

- Ran a follow-up automated audit, connecting directly to the site's own Google Search Console
  property, Ahrefs Site Audit project, and WordPress admin via Claude in Chrome, per the updated
  technical-seo-audit workflow.
- **Confirmed** the 2026-09-06 Cloudflare-blocking finding with real GSC data (16 pages blocked
  403), and found a more direct sign of active harm: DataForSEO's own headless-Chrome render got
  403s on three real page resources (a navigation script, a lazy-load script, a webfont) during
  its own load — Lighthouse Best Practices dropped from 96 to 77 as a result.
- **New finding:** only 14/207 known pages (7%) are indexed by Google — 171 are "discovered" or
  "crawled" but not prioritized for indexing.
- **New finding:** 16 pages with only one incoming internal link, plus an Ahrefs crawl-depth
  warning — the likely structural contributor to the indexing gap above. New fix guide:
  `fixes/site-architecture/ailiabilityguide.com--weak-internal-linking.md`.
- **New finding, missed by the 2026-09-06 2-page sample:** 39 pages missing a meta description
  (the homepage and `/ai-liability/` both happen to have good ones, which masked this). New fix
  guide: `fixes/indexability/ailiabilityguide.com--missing-meta-descriptions.md`.
- **Confirmed at full-site scale, upgraded High:** title-too-long affects 96 of 351 crawled pages
  (27%), not just the one sampled page from 2026-09-06.
- **New finding:** checked the WordPress admin directly — all 184 pages/posts (18 pages + 166
  posts) have no Yoast Focus Keyphrase set, the same pattern found on a different site audited
  through this workflow. New fix guide:
  `fixes/indexability/ailiabilityguide.com--no-focus-keyphrase-set.md`.
- **New, lower-priority findings from Ahrefs:** Open Graph tags incomplete on 207 pages, OG URL
  not matching canonical on 12, plus minor broken-link/redirect/404 counts.
- Not independently re-verified this run (carried forward from 2026-09-06 as still-open):
  security response headers, FAQPage schema.

## 2026-09-06

See `../ailiabilityguide.com-2026-09-06/CHANGELOG.md` for the original audit's log.
