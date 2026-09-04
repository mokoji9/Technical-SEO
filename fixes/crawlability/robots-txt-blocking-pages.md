# Fix Guide: robots.txt Blocking Important Pages

**Category:** Crawlability

## 1. What's wrong

Your `robots.txt` file (a small text file that tells search engines which parts of your site
they're allowed to crawl) is accidentally telling Google "don't visit this page/section" —
even though you want that page indexed and ranking.

## 2. Why it matters

If Google can't crawl a page, it usually can't index it, which means it won't show up in
search results at all — no matter how good the content is. This is one of the most common
"why isn't my page ranking at all" causes.

## 3. How to check it yourself

1. Go to `https://yourdomain.com/robots.txt` in your browser.
2. Look for lines starting with `Disallow:`. Anything listed there is blocked.
3. Example of a page-killing mistake:
   ```
   User-agent: *
   Disallow: /
   ```
   This blocks your **entire site** from every search engine. (Very common accidental mistake
   after moving a site from staging to live.)
4. Also check Google Search Console → **Settings → robots.txt** (or the URL Inspection tool)
   to see if Google reports "blocked by robots.txt" for the page in question.

## 4. Step-by-step fix

1. Open your `robots.txt` file (usually in your site's root folder, or via your CMS's SEO
   settings — e.g. Yoast, Rank Math, Webflow SEO settings).
2. Find the `Disallow:` line blocking the page/folder you want indexed.
3. Either delete that line, or narrow it so it only blocks what you actually want blocked.

   Before (blocks everything):
   ```
   User-agent: *
   Disallow: /
   ```

   After (only blocks admin/staging areas, allows everything else):
   ```
   User-agent: *
   Disallow: /wp-admin/
   Disallow: /staging/
   ```
4. Save and re-upload the file (or save in your CMS).
5. Add your sitemap reference at the bottom if it's missing:
   ```
   Sitemap: https://yourdomain.com/sitemap.xml
   ```

## 5. How to verify the fix worked

1. Revisit `https://yourdomain.com/robots.txt` and confirm the page/folder is no longer
   disallowed.
2. In Google Search Console, use **URL Inspection** on the affected page → click
   **Test Live URL** → confirm it says "Allowed" for crawling.
3. If previously blocked, click **Request Indexing** to speed up recrawl.

## 6. Tools to double-check

- Google Search Console → URL Inspection tool
- [Google robots.txt Tester](https://search.google.com/search-console) (under Settings)
- Any online "robots.txt checker" tool
