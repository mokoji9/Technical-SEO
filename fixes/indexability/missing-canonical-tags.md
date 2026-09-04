# Fix Guide: Missing or Incorrect Canonical Tags

**Category:** Indexability

## 1. What's wrong

A canonical tag tells search engines "this is the master/original version of this page" —
useful when the same or similar content is reachable through multiple URLs
(e.g. `?ref=email`, `www.` vs non-`www`, filtered product listings). Your pages are missing
this tag, or it's pointing to the wrong URL.

## 2. Why it matters

Without a correct canonical, search engines may index the wrong version of a page, split
ranking signals across duplicate URLs, or waste crawl budget on near-identical pages —
weakening your rankings.

## 3. How to check it yourself

1. View page source (Ctrl+U) or Inspect Element on the page.
2. Search for `rel="canonical"` in the `<head>`.
3. It should look like:
   ```html
   <link rel="canonical" href="https://yourdomain.com/page/" />
   ```
4. Confirm the URL it points to is the correct, preferred version (right protocol, right
   www/non-www, no tracking parameters).

## 4. Step-by-step fix

**If using a CMS/SEO plugin:**
1. Most SEO plugins (Yoast, Rank Math, Shopify's built-in SEO) auto-generate canonicals
   correctly by default — check the page's SEO settings for a manual override that might be
   wrong, and remove/correct it.

**If coding manually:**
1. Add this line inside the `<head>` of every page, pointing to the preferred URL:
   ```html
   <link rel="canonical" href="https://yourdomain.com/preferred-page-url/" />
   ```
2. Every variant of a page (with tracking params, filters, etc.) should canonicalize to the
   same clean URL.
3. A page's canonical should point to itself unless it's intentionally a duplicate of another
   page.

## 5. How to verify the fix worked

1. Recheck the page source for the corrected canonical tag.
2. In Google Search Console → URL Inspection, confirm "User-declared canonical" and
   "Google-selected canonical" match your intended URL.
3. Request re-indexing if needed.

## 6. Tools to double-check

- Google Search Console → URL Inspection tool
- Browser "View Page Source"
- Screaming Frog (crawl the site, check the "Canonicals" tab for mismatches at scale)
