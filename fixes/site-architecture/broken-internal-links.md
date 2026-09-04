# Fix Guide: Broken Internal Links (404s)

**Category:** Site Architecture

## 1. What's wrong

Links on your site point to pages that no longer exist (or never existed), returning a 404
error when clicked.

## 2. Why it matters

Broken internal links waste crawl budget, create dead ends for users, and pass no value —
they're pure downside. Enough of them signal a poorly maintained site to both users and
search engines.

## 3. How to check it yourself

1. Crawl the site with a tool like Screaming Frog (or the `screaming-frog-crawler` skill) —
   check the "Response Codes" report, filter for 404s, and look at the "Inlinks" tab to see
   which pages link to each broken URL.
2. Google Search Console → **Page Indexing** report also lists "Not found (404)" pages
   Google has encountered.

## 4. Step-by-step fix

For each broken link found:

1. **Decide the right fix:**
   - If the destination page moved → update the link to the new URL, or add a 301 redirect
     from the old URL to the new one.
   - If the destination page no longer exists and has no equivalent → remove the link
     entirely, or link to the most relevant alternative page.
2. **Fixing the link directly** (preferred — don't rely on redirects alone):
   - Find the broken link in your CMS/page content and update the `href` to the correct URL.
3. **Adding a redirect** (for cases where many external links point to the old URL too):
   ```
   # .htaccess example (Apache)
   Redirect 301 /old-page/ /new-page/
   ```
   or in WordPress, use a redirect plugin (Redirection, Yoast's redirect manager) instead of
   editing `.htaccess` directly.
4. Re-crawl the site to confirm no other pages still link to the old, broken URL.

## 5. How to verify the fix worked

1. Re-crawl the site (Screaming Frog or similar) — confirm the URL now returns 200 (or the
   old URL 301-redirects correctly) and no internal links point to a dead page.
2. Google Search Console → Page Indexing report should show the 404 count decreasing over
   the following days.

## 6. Tools to double-check

- Screaming Frog SEO Spider (or the `screaming-frog-crawler` skill)
- Google Search Console → Page Indexing report
- Any free "broken link checker" tool
