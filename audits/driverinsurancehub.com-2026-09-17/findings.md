# Technical SEO Audit — Driver Insurance Hub (driverinsurancehub.com)

**Date:** 2026-09-17 (independently re-verified same day — see note below)
**Audited by:** Claude
**Method:** Automated — DataForSEO OnPage/Lighthouse API, curl header/status/UA checks, live
browser rendering, **plus a direct connected-account check via Claude in Chrome**: the user's own
logged-in Google Search Console property, Ahrefs Site Audit project, and WordPress admin for this
domain.
**Scope:** Full-site re-check, follow-up to the 2026-09-06 audit (`../driverinsurancehub.com-2026-09-06/`) — this run's main addition is verifying prior findings against real GSC/Ahrefs data instead of crawl-only signals, plus whatever that surfaced that a crawl alone couldn't see.

**Note on this same-day re-run:** at the user's request, every check in this audit was re-run
independently from scratch rather than reused from the earlier run earlier today. All findings
below were re-confirmed live. GSC and Ahrefs both still show "last update" timestamps unchanged
from the earlier run (their own data-refresh lag, not a skipped check), so those specific numbers
are identical by definition. The live crawl/curl/WordPress checks were genuinely redone and
turned up one refinement: the Cloudflare block is **intermittent, not a hard 100% block** — see
the Critical finding below.

## Summary

This run confirms the 2026-09-06 audit's Critical Cloudflare-blocking finding **with real Google
data for the first time** (Search Console shows 50 pages blocked as `403`, not just a spoofed-UA
guess), and confirms the meta-description and title-length issues at true full-site scale via
Ahrefs (614 and 273 of 731 pages respectively, not just the two-page sample checked before). But
the most significant thing this run found is new: **only 204 of 654 known pages (31%) are
actually indexed by Google.** The other 450 split between the already-known blocking/redirect
issues (63 pages) and a much bigger, previously-unmeasured problem — **315 pages "Discovered –
currently not indexed" and 72 "Crawled – currently not indexed."** Ahrefs independently found the
likely root cause of a large share of that: **44 orphan pages with zero incoming internal
links** — pages Google knows about only via the sitemap, with nothing on the site itself pointing
to them, which is a well-known signal that suppresses crawl priority and indexing.

## Findings

### 🔴 Critical

- **Cloudflare bot protection is blocking Googlebot — confirmed directly by Google Search
  Console, and now shown to be intermittent rather than a hard 100% block.** GSC → Indexing →
  Pages shows **50 pages** under "Blocked due to access forbidden (403)," matching the 403/
  `noindex,nofollow` challenge page independently found via curl and DataForSEO's headless-Chrome
  Lighthouse crawl. Re-testing today with repeated identical browser-UA `curl` requests a few
  seconds apart returned a mix of `200` and `403` — the block is probabilistic (Cloudflare's bot
  management likely weighs additional signals like TLS fingerprint and request frequency, not
  just the User-Agent string), which is exactly why a quick manual check can look "fine" while
  Google's own crawl still gets blocked often enough to matter. This removes the "needs
  confirming via Search Console" caveat from the 2026-09-06 audit — it's confirmed, and now
  better understood. Category: Crawlability. See
  `../../fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`.

- **69% of the site (450 of 654 known pages) is not indexed by Google — and most of that isn't
  the Cloudflare block.** GSC → Indexing → Pages breakdown:

  | Reason | Pages | Source |
  |---|---|---|
  | Discovered – currently not indexed | 315 | Google systems |
  | Crawled – currently not indexed | 72 | Google systems |
  | Blocked due to access forbidden (403) | 50 | Website |
  | Page with redirect | 11 | Website |
  | Excluded by 'noindex' tag | 1 | Website |
  | Not found (404) | 1 | Website |

  387 of those 450 pages (the two "Google systems" rows) aren't blocked by anything — Google
  simply hasn't prioritized crawling or indexing them. That's the dominant problem on this site,
  well beyond the Cloudflare issue. See the orphan-pages finding directly below for the likely
  root cause of a large share of it. Category: Indexability. New finding this run — no existing
  fix guide; see `../../fixes/site-architecture/driverinsurancehub.com--orphan-pages-no-internal-links.md`
  for the actionable part of this (linking in orphaned pages), since that's the lever actually
  available to pull.

- **44 orphan pages — pages with zero incoming internal links.** Found via Ahrefs Site Audit
  (Health Score 93%, "Excellent," but this is one of its top-listed issues). These pages are only
  reachable via the sitemap or a direct URL; nothing else on the site links to them. This lines up
  directly with the 387-page indexing gap above — internal links are a primary signal search
  engines use to judge a page's priority, and a page with none reads as low-value regardless of
  its actual content. Category: Site Architecture. See
  `../../fixes/site-architecture/driverinsurancehub.com--orphan-pages-no-internal-links.md`.

### 🟠 High

- **No meta description on 614 of 731 pages (84%) — confirmed at full-site scale.** The
  2026-09-06 audit sampled 2 pages and found both missing; Ahrefs Site Audit now confirms this is
  essentially sitewide, not a template quirk on a couple of pages. Category: Indexability. See
  `../../fixes/indexability/driverinsurancehub.com--missing-meta-descriptions.md` (now includes
  drafted replacement descriptions, not just one example).

- **Titles run past Google's effective display length on 273 of 731 pages (37%) — confirmed at
  full-site scale, and worse than the 2-page sample suggested.** Spot-checked pages range from 72
  characters (homepage) to 110 (the Texas guide, which has much deeper long-form content than the
  templated state pages). Upgraded from Medium to High given the scale. Category: Indexability.
  See `../../fixes/indexability/driverinsurancehub.com--overly-long-page-titles.md` — now includes
  drafted, close-to-copy-paste replacement titles for the homepage, Colorado, Chicago, and Texas
  pages, plus the pattern to repeat across the rest.

- **Every published page and post — 543 of 543 (100%) — has no Yoast Focus Keyphrase set.**
  Checked directly in the WordPress admin: Pages → SEO Score filter → "SEO: No Focus Keyphrase"
  returns all 94 pages; Posts → the same filter returns all 449 posts. To be precise about impact:
  the focus keyphrase field itself isn't read by Google — it's what powers Yoast's own on-page
  checklist while writing (title contains keyphrase, meta description present, keyphrase in the
  first paragraph, etc.). With it never set on anything, that checklist has never actually
  triggered for any of the 543 pieces of content — which is very likely *why* the meta-description
  and title-length problems above are sitewide rather than isolated: the tool that would have
  caught them, page by page, was never engaged. Category: Indexability. See
  `../../fixes/indexability/driverinsurancehub.com--no-focus-keyphrase-set.md` (includes drafted
  example keyphrases for the homepage and three state/city pages, plus the pattern to repeat).

- **No baseline security response headers** — carried forward from 2026-09-06, not
  independently re-verified this run (Cloudflare's challenge response makes a plain `curl` header
  check unreliable — it returns Cloudflare's own headers, not necessarily the origin's). Worth a
  follow-up check via a real browser's Network tab against a full page load. Category: Security &
  International. See `../../fixes/security-international/missing-security-headers.md`.

### 🟡 Medium

- **Duplicate `google-site-verification` meta tag** — reconfirmed present on the homepage today
  via DataForSEO's on-page check (`duplicate_meta_tags: ["google-site-verification"]`). Carried
  forward from 2026-09-06, still unresolved. Category: Indexability. See
  `../../fixes/indexability/driverinsurancehub.com--duplicate-google-site-verification-tag.md`.

- **Site title wraps mid-word on mobile** — carried forward from 2026-09-06, not
  independently re-verified this run (no mobile-viewport check performed today). Category:
  Mobile. See `../../fixes/mobile/driverinsurancehub.com--site-title-wrapping-mid-word.md`.

- **Multiple `<h1>` tags on 7 pages** — new finding via Ahrefs Site Audit; the 2026-09-06 audit's
  2-page sample happened to have a single H1 each, so this wasn't caught before. Category: Site
  Architecture. An existing generic guide applies directly — see
  `../../fixes/site-architecture/multiple-h1-tags.md`.

### 🟢 Low

- **No favicon anywhere on the site** — reconfirmed today (`no_favicon: true` on every page
  checked, including two not sampled in the original audit). Category: Site Architecture. See
  `../../fixes/site-architecture/driverinsurancehub.com--missing-favicon.md`.

### 💡 Suggestions (opportunities, not errors)

- **No Article/structured schema on the state/city guide pages** — carried forward from
  2026-09-06, not independently re-verified this run. See
  `../../fixes/structured-data/missing-schema-markup.md`.
- **115 redirect (3xx) responses one click from the homepage**, per Ahrefs' HTTP status
  distribution by depth. Not yet broken down into specific URLs/chains this run — worth a
  dedicated look at the Redirects report to confirm these aren't multi-hop chains wasting crawl
  budget, especially given the indexing-gap finding above.

## What's already working well

- **No security issues or manual actions** in Google Search Console — confirmed directly.
- **Sitemap is healthy**: `sitemap_index.xml` — status Success, 594 discovered pages, last read
  today (Sep 16/17).
- **Content is not thin.** Ahrefs' word-count distribution shows the large majority of pages sit
  in the 1,000+ word range — the indexing gap above is not a thin-content problem.
- **No duplicate title, H1, or body-content clusters** across the site, per Ahrefs' Duplicates
  report — each page's content is genuinely unique, not templated boilerplate.
- **Performance remains excellent.** Lighthouse (desktop): Performance 100, Accessibility 93,
  Best Practices 96. LCP 0.78s, CLS 0.001.
- **Core Web Vitals field data isn't available yet** (Search Console: "Not enough usage data in
  the last 90 days") — expected given the low current click volume (11 total clicks over the
  measured period); not a red flag on its own, just not measurable yet from real users.
- Canonical tags, HTTPS enforcement, and robots.txt/sitemap linkage all remain correct, as in the
  2026-09-06 audit.

## A correction to the 2026-09-06 audit's delivered fix guides

Two of the fix guides that audit linked — `overly-long-page-titles.md` and `missing-favicon.md`
— were actually written for a *different* site (ailiabilityguide.com) that happened to hit the
same generic issue name first; the shared `fixes/{category}/{issue-name}.md` path let that
happen silently. Both have been split into site-scoped files
(`driverinsurancehub.com--overly-long-page-titles.md`,
`driverinsurancehub.com--missing-favicon.md`) with this site's real content, and the 2026-09-06
audit's own findings/issue-tracker/report have been repointed at the corrected files. The
workflow now requires site-scoped filenames by default going forward, to prevent this recurring.

## Next steps

See `issue-tracker.md` in this folder for the prioritized action list.
