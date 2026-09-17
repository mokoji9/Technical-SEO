# Technical SEO Audit — Driver Insurance Hub (driverinsurancehub.com)

**Date:** 2026-09-06
**Audited by:** Claude
**Method:** Automated (DataForSEO OnPage/Lighthouse API, live browser rendering incl. mobile
viewport, curl header/status/UA checks, robots.txt/sitemap review)
**Scope:** Full sweep — crawlability, indexability, site architecture, performance, mobile,
structured data, security/international

## Summary

Same hosting stack as a previous audit in this workflow (WordPress + Yoast SEO + Cloudflare, on
Bluehost) and the same critical problem shows up: **Cloudflare's bot protection is serving a JS
challenge page — HTTP 403 with an explicit `noindex,nofollow` — to non-browser requests**,
confirmed independently by a spoofed Googlebot user-agent and by DataForSEO's own headless-Chrome
Lighthouse crawler. That needs the same Search Console confirmation before touching Cloudflare
settings. Beyond that, this site has its own distinct set of gaps: **every page checked is
missing a meta description entirely** (which is also producing a broken-looking `[…]` snippet in
social previews), a real mobile bug where the site name visibly breaks mid-word in the header,
a duplicated Search Console verification tag, and titles running past Google's display limit.
Performance and accessibility are strong across the board, same as the earlier audit.

## Findings

### 🔴 Critical

- **Cloudflare bot protection is challenging/blocking non-browser crawl requests** — a spoofed
  Googlebot user-agent got HTTP 403 on both the homepage and `/sitemap_index.xml`, and
  DataForSEO's Lighthouse run recorded the main document request returning HTTP 403 while
  rendering a page containing `<meta name="robots" content="noindex,nofollow">` — Cloudflare's
  interstitial challenge, not the real site. Category: Crawlability. See
  `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`. **Needs confirming via
  Google Search Console → URL Inspection → Test Live URL** before changing Cloudflare settings —
  Cloudflare's Verified Bots allowlist may already let the real Googlebot through.

### 🟠 High

- **No meta description on any page checked.** Both the homepage and a sampled state page
  (`/colorado-rideshare-insurance-for-uber-lyft-drivers/`) are flagged `no_description` — there's
  no `<meta name="description">` tag at all, not just an empty one. As a side effect, the
  Open Graph description falls back to WordPress's auto-excerpt, which cuts off mid-sentence with
  a literal `[…]` — visible in social share previews. Category: Indexability. See
  `fixes/indexability/driverinsurancehub.com--missing-meta-descriptions.md`.
- **No baseline security response headers anywhere.** Checked headers on the homepage: no
  `Strict-Transport-Security`, `Content-Security-Policy`, `X-Frame-Options`,
  `X-Content-Type-Options`, or `Referrer-Policy`. Category: Security & International. See
  `fixes/security-international/missing-security-headers.md`.

### 🟡 Medium

- **Site title wraps mid-word on mobile.** At a 375px mobile viewport, the header's site name
  renders as "Driver / Insura / nce / Hub" — breaking mid-word instead of at spaces — because the
  Astra theme's site-identity element has `overflow-wrap: anywhere` applied inside a header
  column that's too narrow at this breakpoint. Visible on every page, above the fold, on every
  mobile visit. Category: Mobile. See `fixes/mobile/driverinsurancehub.com--site-title-wrapping-mid-word.md`.
- **Duplicate `google-site-verification` meta tag.** The same verification value appears twice
  in the homepage `<head>`. Harmless today, but a sign of overlapping theme/plugin configuration
  worth cleaning up. Category: Indexability. See
  `fixes/indexability/driverinsurancehub.com--duplicate-google-site-verification-tag.md`.
- **Titles run past Google's effective display length.** Homepage title is 72 characters
  ("Rideshare Insurance Guide for Uber & Lyft Drivers - Driver Insurance Hub"); the Colorado state
  page is 75 characters. Both flagged `title_too_long`, and the pattern likely repeats across all
  ~50 state guide pages, which share the same title template. Category: Indexability. See
  `fixes/indexability/driverinsurancehub.com--overly-long-page-titles.md`.

### 🟢 Low

- **No favicon anywhere on the site.** Confirmed by inspecting the rendered DOM (no
  `<link rel="icon">`) and by the `no_favicon` flag on every page checked. Category: Site
  Architecture. See `fixes/site-architecture/driverinsurancehub.com--missing-favicon.md`.

### 💡 Suggestions (opportunities, not errors)

- **No Article/structured schema on the ~50 state guide pages.** Each state page is genuine,
  purpose-built long-form content (requirements, coverage, cost, recommendations per state), but
  JSON-LD only carries Yoast's default `WebPage`/`WebSite`/`BreadcrumbList` graph — no `Article`
  type. Adding it is low-effort given how templated these pages already are, and improves how AI
  answer engines and Google understand each page's subject/date/authorship. See
  `fixes/structured-data/missing-schema-markup.md`.

## What's already working well

- **HTTPS is fully enforced.** Plain HTTP requests get a clean WordPress-issued 301 to HTTPS.
- **robots.txt and sitemap are valid and correctly linked** — Yoast-generated, no accidental
  Disallow rules, sub-sitemaps for posts/pages/categories all present.
- **Canonical tags are correct** on every page checked, including the state guide template pages.
- **Performance is excellent.** Lighthouse Performance: 100. LCP 0.76s, CLS 0.001 — no Core Web
  Vitals concerns.
- **Accessibility (93) and Best Practices (96) score well**, consistent with a clean, modern
  WordPress + Astra build.
- **Content is genuinely structured for the topic** — a clear state-by-state architecture with
  descriptive URLs (`/colorado-rideshare-insurance-for-uber-lyft-drivers/`) that match how people
  actually search this topic.
- **Single H1 per page, descriptive internal links** — Lighthouse's `link-text` and
  `crawlable-anchors` SEO audits both pass.

## Next steps

See `issue-tracker.md` in this folder for the prioritized action list.
