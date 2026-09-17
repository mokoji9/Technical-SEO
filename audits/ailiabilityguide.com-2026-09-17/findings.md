# Technical SEO Audit — AI Liability Guide (ailiabilityguide.com)

**Date:** 2026-09-17
**Audited by:** Claude
**Method:** Automated — DataForSEO OnPage/Lighthouse API, curl header/status/UA checks, live
browser rendering, **plus a direct connected-account check via Claude in Chrome**: the user's own
logged-in Google Search Console property, Ahrefs Site Audit project, and WordPress admin for
this domain.
**Scope:** Full-site re-check, follow-up to the 2026-09-06 audit
(`../ailiabilityguide.com-2026-09-06/`) — verifying prior findings against real GSC/Ahrefs/
WordPress data instead of a small crawl sample, plus whatever that surfaced that a 2-page sample
couldn't see.

## Summary

The Cloudflare bot-blocking finding from 2026-09-06 is now **confirmed directly by Google Search
Console** (16 pages blocked as `403`), and it's worse than a challenge page shown to bots: even
DataForSEO's own real headless-Chrome render got **403s on specific page resources** — a
navigation script, an image lazy-loader script, and a webfont — meaning Cloudflare is actively
breaking parts of the page for some real, JS-executing requests, not just presenting a "prove
you're human" screen. Beyond that, the most significant new finding is the same shape as a
parallel audit on a different site run through this workflow: **only 14 of 207 known pages (7%)
are indexed by Google** — worse than the other site's 31%. 171 pages are "discovered" or
"crawled" but not prioritized for indexing, and Ahrefs found a related structural signal: 16
pages reachable by only one internal link, plus a crawl-depth warning that the site has pages
sitting considerably far from the homepage. Also confirmed at true full-site scale via Ahrefs
(the 2026-09-06 audit only sampled 2 pages, which happened to look fine): 39 pages missing a
meta description, and 96 of 351 crawled pages (27%) with an overly long title — both much larger
than the earlier sample suggested. And checking the WordPress admin directly found all 184
pages/posts have no Yoast Focus Keyphrase set, the same pattern found on the other audited site.

## Findings

### 🔴 Critical

- **Cloudflare bot protection is blocking Googlebot — confirmed directly by Google Search
  Console, and now shown to break specific page resources too.** GSC → Indexing → Pages shows
  **16 pages** under "Blocked due to access forbidden (403)." Separately, DataForSEO's Lighthouse
  run — a real headless-Chrome render, not a UA spoof — logged three resource requests failing
  with 403 during the page's own load: `wp-includes/js/.../navigation/view.min.js`, the Bluehost
  plugin's `image-lazy-loader.min.js`, and the theme's `cardo_normal_400.woff2` webfont. This is a
  more direct sign of active breakage than a bot-only challenge page — Lighthouse's Best Practices
  score dropped from 96 (2026-09-06) to 77 largely because of these console errors. Category:
  Crawlability. See `../../fixes/crawlability/cloudflare-bot-protection-blocking-crawlers.md`.

- **93% of known pages (193 of 207) are not indexed by Google.** GSC → Indexing → Pages
  breakdown:

  | Reason | Pages | Source |
  |---|---|---|
  | Discovered – currently not indexed | 151 | Google systems |
  | Crawled – currently not indexed | 20 | Google systems |
  | Blocked due to access forbidden (403) | 16 | Website |
  | Excluded by 'noindex' tag | 4 | Website |
  | Page with redirect | 2 | Website |

  171 of those pages (the two "Google systems" rows) aren't blocked by anything specific — Google
  hasn't prioritized crawling or indexing them. Category: Indexability. New finding this run — no
  existing fix guide directly targets the indexing-gap number itself; see the weak-internal-linking
  finding below for the structural lever available to pull.

- **16 pages reachable by only one internal link, and Ahrefs flags the crawl as incomplete due
  to pages sitting far from the homepage.** Ahrefs' "Page has only one dofollow incoming internal
  link" issue (16 indexable + 9 non-indexable), plus its own banner: *"The website may not be
  fully crawled... you might want to check why some of the URLs on your website are considerably
  distant from the seed."* This isn't as severe as a true orphan page (found on the other site
  audited through this workflow), but it's the same category of problem and lines up with the
  171-page indexing gap above. Category: Site Architecture. See
  `../../fixes/site-architecture/ailiabilityguide.com--weak-internal-linking.md`.

### 🟠 High

- **39 pages missing a meta description, 2 with one too long — a real issue the 2026-09-06
  2-page sample missed entirely** (the homepage and `/ai-liability/` both happen to have good
  descriptions, which masked this). Confirmed via Ahrefs Site Audit: 23 indexable + 16
  non-indexable pages with none, 2 with one too long. Category: Indexability. See
  `../../fixes/indexability/ailiabilityguide.com--missing-meta-descriptions.md` (includes drafted
  replacement descriptions matching the site's existing working examples).

- **Titles run past Google's effective display length on 96 of 351 crawled pages (27%) —
  confirmed at full-site scale, upgraded from Medium to High.** The 2026-09-06 audit found one
  95-character title on `/ai-liability/` and noted the pattern "likely repeats" — Ahrefs now
  confirms it does, at a larger scale than a single sample implied. Category: Indexability. See
  `../../fixes/indexability/ailiabilityguide.com--overly-long-page-titles.md`.

- **Every page and post — 184 of 184 (100%) — has no Yoast Focus Keyphrase set.** Checked
  directly in the WordPress admin: Pages → SEO Score filter → "SEO: No Focus Keyphrase" returns
  all 18 pages; Posts → same filter returns all 166 posts. Same finding, same root-cause logic, as
  a parallel audit of a different site run through this workflow: the keyphrase field itself
  isn't read by Google, but it's what powers Yoast's on-page checklist, which has never actually
  triggered for any of this site's content either. Category: Indexability. See
  `../../fixes/indexability/ailiabilityguide.com--no-focus-keyphrase-set.md`.

- **No baseline security response headers** — carried forward from 2026-09-06, not independently
  re-verified this run (Cloudflare's challenge/edge responses make a plain `curl` header check
  unreliable for this domain). Category: Security & International. See
  `../../fixes/security-international/missing-security-headers.md`.

### 🟡 Medium

- **FAQ content exists but isn't marked up as `FAQPage` schema** — carried forward from
  2026-09-06, not independently re-verified this run. Category: Structured Data. See
  `../../fixes/structured-data/missing-schema-markup.md`.
- **Open Graph tags incomplete on 207 pages, and 12 pages have an Open Graph URL that doesn't
  match the canonical.** New finding via Ahrefs Site Audit — not previously checked. Lower
  priority than the indexing/content issues above, but worth a look since it affects how pages
  render when shared on social platforms. Category: Structured Data / Social.
- **Minor link/status issues:** 1 page linking to a broken page pair (2 instances), 1 confirmed
  404, 1 other 4xx, 5 pages with a 3xx redirect. Small in volume; worth cleaning up alongside the
  other fixes rather than a dedicated project.

### 🟢 Low

- **No favicon anywhere on the site** — reconfirmed today (`no_favicon: true` on both the
  homepage and `/ai-liability/`). Category: Site Architecture. See
  `../../fixes/site-architecture/ailiabilityguide.com--missing-favicon.md`.

### 💡 Suggestions (opportunities, not errors)

- **Content reads at a very high complexity level** — reconfirmed today (homepage
  Flesch-Kincaid -24.1, `/ai-liability/` -25.9, both effectively unchanged from 2026-09-06). Not
  a technical defect — an editorial call about audience fit.
- **GSC and Ahrefs disagree on the noindex count** (GSC: 4 pages excluded by noindex tag; Ahrefs:
  16 noindex pages found in its crawl). Likely a scope difference — Ahrefs may be crawling
  category/tag/attachment pages outside the sitemap that GSC doesn't report on separately. Worth
  a quick look to confirm nothing unexpected is noindexed.

## What's already working well

- **No security issues or manual actions** in Google Search Console — confirmed directly.
- **Sitemap is healthy**: `sitemap_index.xml` — status Success, 195 discovered pages, last read
  Sept 11.
- **No duplicate content, title, or H1 clusters** flagged by Ahrefs.
- **Performance remains excellent.** Lighthouse: Performance 100, Accessibility 100
  (up from 93), SEO 100. LCP 0.59s, CLS 0.001.
- **HTTPS enforcement, robots.txt/sitemap validity, and canonical tags** all remain correct, as
  in the 2026-09-06 audit.
- **The site's working meta descriptions (homepage, `/ai-liability/`) show the right voice and
  length** — this is a real, usable pattern, not a site starting from zero.

## Next steps

See `issue-tracker.md` in this folder for the prioritized action list.
