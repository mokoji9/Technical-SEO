# Technical SEO Audit — AI Liability Guide (ailiabilityguide.com)

**Date:** 2026-09-06
**Audited by:** Claude
**Method:** Automated (DataForSEO OnPage/Lighthouse API, live browser rendering, curl header/status/UA checks, robots.txt/sitemap review)
**Scope:** Full sweep — crawlability, indexability, site architecture, performance, mobile, structured data, security/international

## Summary

The site itself is fast, clean, and well-structured (Lighthouse Performance 100, Best Practices
96, Accessibility 93) with correct canonical tags, a valid Yoast-generated sitemap, and a
genuinely good mobile layout. But there's one critical problem sitting in front of all of that:
**Cloudflare's bot protection is serving a JS "Just a moment…" challenge page — complete with an
explicit `noindex,nofollow` and HTTP 403 — to non-browser requests, including a spoofed
Googlebot user-agent and DataForSEO's own headless-Chrome crawler.** That's the single biggest
risk to this site's visibility, and it needs confirming against Google Search Console directly
(see the Critical finding below for why). Everything else found is comparatively minor:
missing baseline security headers, missing FAQ structured data despite having FAQ content ready
to mark up, a few overly long titles, and a missing favicon.

## Findings

### 🔴 Critical

- **Cloudflare bot protection is challenging/blocking non-browser crawl requests, including a
  simulated Googlebot and an automated SEO crawler** — `curl` with a spoofed Googlebot
  user-agent got HTTP 403 on both the homepage and `/sitemap_index.xml`. More importantly,
  DataForSEO's own Lighthouse run (real headless Chrome, not a simple UA spoof) recorded the
  main document request returning **HTTP 403** and rendered a page containing
  `<meta name="robots" content="noindex,nofollow">` — that's Cloudflare's interstitial
  challenge page, not the real site. A plain `curl` with no user-agent at all also got 403 on a
  fresh, uncached request. Real browsers (this session's rendering browser, and presumably most
  human visitors) sail through fine, which is exactly what makes this invisible day-to-day.
  Category: Crawlability. See `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`.
  **Needs confirming via Google Search Console → URL Inspection → Test Live URL** before
  concluding real Googlebot (not a spoofed UA) is actually affected — Cloudflare has a
  "Verified Bots" allowlist that can let Google's real IPs through even while blocking
  everything else, so this is a strong signal, not yet 100% proof against the real crawler.

### 🟠 High

- **No baseline security response headers anywhere on the site.** Checked headers on the
  homepage and `/ai-liability/`: no `Strict-Transport-Security`, no `Content-Security-Policy`,
  no `X-Frame-Options`, no `X-Content-Type-Options`, no `Referrer-Policy`. The site is
  Cloudflare-fronted, so these can be added at the edge without touching WordPress. Category:
  Security & International. See `fixes/security-international/missing-security-headers.md`.

### 🟡 Medium

- **FAQ content exists but isn't marked up as `FAQPage` schema.** `/ai-liability/` (and likely
  the other pillar pages, which follow the same template) has a visible "Frequently Asked
  Questions" section with 5 Q&As, but the page's JSON-LD only includes Yoast's default
  `WebPage`/`WebSite`/`BreadcrumbList` graph — no `FAQPage` entity. This is a missed rich-result
  opportunity that's low-effort to add since the content is already written. Category:
  Structured Data. See `fixes/structured-data/missing-schema-markup.md`.
- **Page titles run well past Google's effective display length.** `/ai-liability/`'s title is
  95 characters ("AI Liability: Who Is Responsible When Artificial Intelligence Causes Harm? -
  AI Liability Guide"), flagged by the on-page check as `title_too_long`. The homepage's title
  page pattern (full question/headline + " - AI Liability Guide") likely repeats across the
  other pillar and article pages. Category: Indexability. See
  `fixes/indexability/ailiabilityguide.com--overly-long-page-titles.md`.

### 🟢 Low

- **No favicon anywhere on the site.** Confirmed by inspecting the rendered DOM (no
  `<link rel="icon">` at all) and by DataForSEO's `no_favicon` flag on every page checked. Minor
  polish/completeness item — costs nothing to add. Category: Site Architecture. See
  `fixes/site-architecture/ailiabilityguide.com--missing-favicon.md`.

### 💡 Suggestions (opportunities, not errors)

- **Content reads at a very high complexity level.** Readability metrics are consistently
  extreme across pages checked — e.g. `/ai-liability/`'s Flesch-Kincaid score is -25.9 (the
  scale normally runs 0-100; negative means extremely dense, long-sentence, jargon-heavy text)
  and its Automated Readability Index is 23 (roughly "graduate/professional" reading level).
  That may be appropriate for the target audience (compliance/legal/risk professionals), but
  it's worth a deliberate check that it's not accidentally alienating a broader audience
  searching for plain-language answers — AI-driven answer engines in particular tend to favor
  content that states its point directly before elaborating. Not a technical defect, so no fix
  guide — a content/editorial call.

## What's already working well

- **HTTPS is fully enforced.** Plain `http://` requests get a clean 301 (`X-Redirect-By:
  WordPress`) straight to `https://`, and every page checked reports `is_https: true`.
- **robots.txt and sitemap are valid and correctly linked.** Yoast-generated, points to
  `sitemap_index.xml` → three well-formed sub-sitemaps (post/page/category). No accidental
  `Disallow` rules.
- **Canonical tags are correct everywhere, including the tricky case.** The homepage's WordPress
  query-loop pagination (`/?query-2-page=2`, `/3`, … up to `/28`) all self-canonicalize back to
  `/`, which is exactly right and avoids a duplicate-content problem that's easy to get wrong on
  paginated homepages.
- **Performance is excellent.** Lighthouse Performance score: 100. LCP 0.77s, CLS 0.001, Total
  Blocking Time 3ms, server response time 49ms — no Core Web Vitals concerns at all.
  Accessibility (93) and Best Practices (96) also score well.
- **Mobile layout is clean.** Checked at 375×812 (mobile viewport): responsive text, no
  horizontal overflow, no cramped tap targets, correct `viewport` meta tag.
  content.
- **Single H1 per page, descriptive internal link text, all links crawlable** — Lighthouse's
  `link-text` and `crawlable-anchors` SEO audits both pass cleanly.
- **Some structured data already present.** Yoast's default `WebPage`/`WebSite`/
  `BreadcrumbList` JSON-LD is in place site-wide — the gap is specifically the missing
  `FAQPage` markup noted above, not a total absence of schema.

## Next steps

See `issue-tracker.md` in this folder for the prioritized action list.
