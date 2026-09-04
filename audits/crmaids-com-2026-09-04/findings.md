# Technical SEO Audit — crmaids.com

**Date:** 2026-09-04
**Audited by:** Claude (automated)
**Method:** Automated — DataForSEO OnPage/Lighthouse API, live browser checks (Claude Browser), curl (status codes, headers, redirect chains, bot vs. browser UA), WebFetch of robots.txt/sitemaps
**Scope:** Full site — homepage deep-dive, robots.txt, sitemap index + all 7 sub-sitemaps, spot-checks of internal links and a sample blog URL

## Summary

The site is technically solid on security, HTTPS, and structured data, and Lighthouse SEO
scores a perfect 100. But there's one **critical, confirmed** crawlability bug: two of the
site's seven sitemap files — the ones listing WordPress **Pages** (as opposed to blog posts) —
return a server timeout/500 error instead of XML, on every attempt, from both `curl` and a real
browser, across two separate audit passes run the same day. That's very likely contributing to
pages not getting picked up or refreshed via sitemap. Beyond that, the homepage is overweight
(~7.8-8.0MB) due to several uncompressed JPEGs, which is dragging Core Web Vitals down, and the
viewport tag blocks pinch-zoom.

## Findings

### 🔴 Critical

- **`page-sitemap1.xml` and `page-sitemap2.xml` return a 500 timeout instead of the sitemap** —
  Category: Crawlability. See `fixes/crawlability/sitemap-file-timeout-error.md`.
  - `https://crmaids.com/sitemap_index.xml` loads fine and lists 7 sub-sitemaps, two of which
    (`page-sitemap1.xml`, `page-sitemap2.xml`) are the most recently updated (2026-09-03,
    the day before this audit) — these are the WordPress "Pages" sitemaps, which typically hold
    the site's core service/location pages rather than blog content.
  - Tested **5 separate times across two audit passes** the same day, with `curl` (default UA,
    Googlebot UA) and a real browser (Claude Browser) — every single attempt returned
    **`Status: 000`, no bytes received, after a 20-30s timeout**, with zero variance between
    runs.
  - Confirmed independently in a real browser: navigating directly to `page-sitemap1.xml`
    rendered LiteSpeed's own error page: *"500 Internal Server Error — Request Timeout — This
    request takes too long to process, it is timed out by the server."*
  - The other 5 sitemaps (`post-sitemap1-4.xml`, `local-sitemap.xml`) load normally and fast,
    both times tested.
  - This is a server-side bug (most likely the sitemap generator timing out building entries
    for these pages, or a caching/optimization plugin interfering with the dynamic XML
    endpoint) — not something fixable by editing the sitemap file itself. See the fix guide for
    the specific things to check with your host.

### 🟠 High

- **Homepage total page weight is ~7.8-8.0MB, and Largest Contentful Paint (LCP) is 5.1-6.0s** —
  Category: Performance. See `fixes/performance/unoptimized-images.md`.
  - Lighthouse Performance score: **0.54-0.56 / 1.0** across three runs today.
  - LCP ranged 5.1s-6.0s across runs — all well outside Google's "good" threshold of ≤2.5s.
  - Root cause confirmed directly: several JPEG images uploaded in August 2026
    (`IMG_5057-scaled.jpg`, `83ad71b4...-scaled.jpg`, `IMG_2638-scaled.jpeg`, and others in the
    same batch) are **~620-640KB each** and load uncompressed/unconverted on the homepage,
    despite the site already using WebP elsewhere for other images. These few files alone
    account for roughly 1.9MB+ of the page's weight.
  - 8 render-blocking resources were also flagged on the same page load — see
    `fixes/performance/render-blocking-resources.md`.

### 🟡 Medium

- **Cumulative Layout Shift (CLS) is 0.178**, consistent across every run today — Category:
  Performance. Google's "good" threshold is ≤0.1 (this falls in the "needs improvement" band,
  not yet "poor"). Once the oversized images above are given explicit width/height (see the
  image fix guide), this typically drops along with the byte-weight fix.

- **Viewport meta tag disables pinch-to-zoom** — Category: Mobile. See
  `fixes/mobile/missing-viewport-meta.md` (covers this exact case).
  - Homepage viewport tag is: `width=device-width, initial-scale=1.0, maximum-scale=1.0,
    user-scalable=0`.
  - `user-scalable=0` blocks visitors from pinch-zooming to read small text — an accessibility
    issue (WCAG 1.4.4) that Google's mobile-usability signals also penalize.
  - Reflected in the Lighthouse Accessibility score of 0.89/1.0 (not a perfect 100).

### 🟢 Low

- **`robots.txt` has two separate, redundant `User-agent: *` blocks**, and disallows several
  paths (`/admin/`, `/provider/`, `/qbconnect/`, `/live-reviews/`, etc.) that look like leftover
  rules from a different (non-WordPress) app structure, alongside a second, WordPress-specific
  block with `Allow: /`. Most crawlers merge same-UA rule groups correctly, so this likely isn't
  actively breaking anything today, but it's worth a cleanup pass — remove/consolidate stale
  rules so future edits don't accidentally reintroduce a real blocking issue. Also worth
  double-checking that `Disallow: /images/` isn't intended to (and doesn't accidentally) block
  Google Images from indexing photos, since actual image files are served from
  `/wp-content/uploads/`, not `/images/`.
  See `fixes/crawlability/robots-txt-blocking-pages.md` for how to audit and test robots.txt
  rules.

- **`/contact` 301-redirects to `/contact/`** — Category: Site architecture. A trailing-slash
  normalization redirect. Not harmful, but any internal links pointing to `/contact` (without
  the slash) cost an extra hop. Quick win: update internal links to point directly to the
  canonical `/contact/`.

- **Three duplicate `<meta name="generator">` tags** (WordPress, Site Kit by Google, WP Rocket)
  plus a duplicated `ti-site-data` tag, flagged by the on-page scanner as duplicate meta tags.
  Cosmetic/technically-invalid-HTML issue only — doesn't affect rankings, low priority.

### 💡 Suggestions

- **No `LocalBusiness`/`Organization` schema detected** — Category: Structured data. See
  `fixes/structured-data/missing-schema-markup.md`. The homepage already has good `FAQPage`,
  `Service`, and `WebSite` (with `SearchAction`) schema, plus `Place`/`GeoCoordinates`/
  `PostalAddress` data nested in there — but there's no explicit `LocalBusiness` type carrying
  the business's name, address, phone, and hours as a first-class entity. For a local cleaning
  service, this is a real opportunity for Google's local pack / rich results (star ratings,
  business info in search) — not a defect, but worth adding.

- **Heavy third-party script footprint** — the homepage loads Google Tag Manager, Facebook
  Pixel, Microsoft/Bing UET, Google/DoubleClick Ads, Microsoft Clarity, an Elfsight widget,
  GoHighLevel/LeadConnector, and a UserWay accessibility widget. Each adds network overhead on
  top of the image-weight problem above. Worth an audit of which are still actively used, and
  loading the non-critical ones after first paint (e.g. via Google Tag Manager's built-in
  trigger delays) once the image fix is in.

## What's working well (no action needed)

- **Security & HTTPS**: HTTP → HTTPS forced (301), `www` → apex canonicalized (301), HSTS with
  `preload` and a 1-year max-age, and a strong header set (CSP, X-Frame-Options,
  X-Content-Type-Options, Referrer-Policy, Permissions-Policy, X-XSS-Protection). Nothing to fix
  here. Re-verified identical on a second pass.
- **Indexability basics**: self-referencing canonical tag present, meta robots correctly set to
  `index, follow` with sensible snippet/preview directives, single canonical domain enforced.
- **Sitemap index & 5 of 7 sub-sitemaps**: `sitemap_index.xml`, all 4 `post-sitemap` files
  (200 URLs total, sampled URL returns 200), and `local-sitemap.xml` all load correctly and are
  correctly referenced from `robots.txt`.
- **Lighthouse SEO score: 1.0 / 1.0** on the homepage, consistent across all runs.
- **Structured data**: `FAQPage`, `Service`, and `WebSite`/`SearchAction` schema present and
  well-formed.
- **Image alt text on sampled images**: the images spot-checked directly in the raw HTML had
  descriptive `alt` text (the on-page scanner did flag a site-wide "missing alt" signal — worth
  a fuller image-by-image audit, but this isn't a wholesale failure like it can be on some
  sites).
- **404 handling**: a genuinely non-existent URL correctly returns a real 404, not a soft-404.
- **Bot access**: identical response (200, same content) to a spoofed Googlebot user-agent and a
  normal browser user-agent on the homepage — no evidence of cloaking or bot-blocking, unlike
  what's sometimes seen with aggressive bot-protection services.

## Next steps

See `issue-tracker.md` in this folder for the prioritized action list.
