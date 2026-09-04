# Fix Guide: Missing or Incorrect Viewport Meta Tag

**Category:** Mobile

## 1. What's wrong

The page is missing the viewport meta tag (or has it configured incorrectly), which tells
mobile browsers how to scale and display the page. Without it, mobile browsers render the
page as if on desktop and then shrink it — making text tiny and hard to read.

## 2. Why it matters

Google uses mobile-first indexing — it primarily evaluates the mobile version of your site
for ranking. A broken mobile experience directly hurts rankings, not just user experience.

## 3. How to check it yourself

1. View page source (Ctrl+U), search for `viewport`.
2. It should look like:
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1">
   ```
3. If missing, or if it has strange values (e.g. a fixed pixel width, or
   `user-scalable=no`), that's the issue.
4. Test on [Google's Mobile-Friendly Test](https://search.google.com/test/mobile-friendly).

## 4. Step-by-step fix

1. Add this line inside the `<head>` of every page template:
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1">
   ```
2. Avoid `user-scalable=no` or `maximum-scale=1` — these block users from pinch-zooming,
   which is both an accessibility issue and something Google flags negatively.
3. If using a CMS, this is usually in the site-wide header/theme template
   (`header.php` in WordPress themes, or global site settings in Webflow/Shopify) — it
   should only need to be set once, not per-page.

## 5. How to verify the fix worked

1. Re-run [Google's Mobile-Friendly Test](https://search.google.com/test/mobile-friendly) —
   should now pass.
2. Open the page on an actual phone (or Chrome Dev Tools → Toggle device toolbar) and
   confirm text is readable without zooming and nothing overflows horizontally.

## 6. Tools to double-check

- [Google Mobile-Friendly Test](https://search.google.com/test/mobile-friendly)
- Chrome Dev Tools → Device Toolbar (mobile emulation)
- Google Search Console → Mobile Usability report
