# Technical SEO Audit — islandroute.io

**Date:** 2026-09-04
**Audited by:** Claude (automated)
**Method:** Automated — DataForSEO OnPage/Lighthouse API, live browser checks (Claude Browser), curl user-agent tests, WebFetch
**Scope:** Homepage (`https://www.islandroute.io/`), sitemap.xml, spot-check of `/old-home`

## Summary

Core performance and on-page basics (title, meta description, canonical, viewport) are solid —
Lighthouse Performance 94, SEO 100, Best Practices 100. But there's one serious, needs-verification
issue: **Cloudflare bot protection appears to be blocking or challenging automated crawlers**,
which could be affecting Googlebot too. That's the top priority to confirm and fix. Beyond that,
the main gaps are missing image alt text and a thin/placeholder page sitting in the live sitemap.

## Findings

### 🔴 Critical

- **Cloudflare bot protection may be blocking search engine crawlers** — Category: Crawlability.
  See `fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`.
  - DataForSEO's OnPage crawler (JS-rendering enabled) got a flat **403 Forbidden** fetching the
    homepage.
  - `curl` with a `Googlebot/2.1` user-agent → **403**. Same `curl` with a normal Chrome
    desktop user-agent → **200**. Plain `curl` (no browser UA) → **403**.
  - A real browser session (Claude Browser, full JS) was served Cloudflare's
    **"Just a moment... / Verify you are human"** interstitial challenge page on one visit
    (page `<title>` was literally "Just a moment...", with `<meta name="robots"
    content="noindex,nofollow">` on that interstitial). A subsequent visit passed through to
    real content automatically.
  - This is inconsistent — some requests get real content, some get challenged or flat-out
    blocked. Googlebot cannot solve interactive challenges, so if it's hitting this challenge
    or being blocked, pages can silently stop getting crawled/indexed.

### 🟠 High

- **51 of 54 images on the homepage are missing `alt` text** — Category: On-page content
  (accessibility + image SEO). Contributes to the Lighthouse Accessibility score of 85/100
  (not 100). No dedicated fix guide yet — see Suggestions below for adding an "on-page content"
  checklist category to cover this going forward. Quick fix: audit `<img>` tags site-wide and
  add descriptive `alt` attributes.

### 🟡 Medium

- **`/old-home` is a thin, placeholder-style page still live and listed in `sitemap.xml`** —
  Category: Indexability / Site architecture. Content is just "THE TREASURE HUNT IS STARTING
  SOON" + a sign-up button — looks like an abandoned/legacy page, not real content. Being in
  the sitemap tells Google to crawl and index it as if it were a real page, which dilutes site
  quality signals. Recommend either: redirect it (301) to the relevant live page, add
  `noindex`, or remove it from the sitemap if it's meant to stay live but not ranked.

- **Only one structured data type present (`WebSite`)** — Category: Structured data. For a
  travel/tourism product like this, there's a real opportunity to add `Organization` (or
  `TravelAgency`/`TouristTrip`) and `FAQPage` schema (the site already has `/faq` and
  `/mauritius-faq` pages — those are prime FAQPage schema candidates for rich results).

### 🟢 Low

- **Every URL in `sitemap.xml` shares the identical `lastmod` date (2026-03-16)**, including
  static pages like Terms & Conditions and dynamic-sounding ones like `/posts`. Suggests the
  sitemap is generated once rather than reflecting real update dates — low priority, but worth
  automating if the sitemap generator supports it.

### 💡 Suggestions

- Lighthouse's newer **"Agentic Browsing"** category (how well the site works for AI
  browsing agents / WebMCP) scored 50/100. This is an emerging, optional area — not an
  established ranking factor yet, but worth keeping an eye on given the AI-search direction
  this repo's `geo-content-optimizer` skill is built for.
- Repo improvement: consider adding an 8th checklist category — **On-Page Content** (title
  tags, meta descriptions, heading structure, image alt text) — since findings like the missing
  alt text above don't map cleanly to the current 7 categories.

## What's working well (no action needed)

- Lighthouse: Performance 94, Best Practices 100, SEO 100
- LCP 1.28s, CLS 0.05, TBT 10ms — all comfortably within "good" Core Web Vitals thresholds
- Title, meta description, canonical tag, and viewport meta tag all present and correct on
  homepage
- Mobile layout renders cleanly (checked at 375×812)
- `robots.txt` is clean and correctly references the sitemap
- HTTPS enforced

## Next steps

See `issue-tracker.md` in this folder for the prioritized action list.
