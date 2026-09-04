# Fix Guide: Accidental "noindex" on Important Pages

**Category:** Indexability

## 1. What's wrong

A page has a `noindex` instruction (in the HTML `<head>` or in an HTTP header) telling search
engines "don't include this page in search results" — but you actually want it to rank.

## 2. Why it matters

A `noindex`'d page will never appear in Google search results, no matter how good its
content or links are. This is one of the most common causes of "my whole site/section
disappeared from Google" — often left over from a staging site going live.

## 3. How to check it yourself

1. View page source (Ctrl+U), search for `noindex`. Look for:
   ```html
   <meta name="robots" content="noindex">
   ```
2. Also check HTTP response headers (Dev Tools → Network tab → click the page request →
   Headers) for:
   ```
   X-Robots-Tag: noindex
   ```
3. In Google Search Console → **Page Indexing** report, look for "Excluded by 'noindex' tag."

## 4. Step-by-step fix

**If using a CMS:**
1. WordPress: check **Settings → Reading → "Discourage search engines from indexing this
   site"** is unchecked (very common accidental cause).
2. In the page's SEO plugin settings (Yoast/Rank Math), check the "noindex" toggle for that
   specific page/post and turn it off.

**If coding manually:**
1. Remove or change this line in the page's `<head>`:
   ```html
   <meta name="robots" content="noindex">
   ```
   to:
   ```html
   <meta name="robots" content="index, follow">
   ```
2. If it's set via server/HTTP header (common on staging environments), remove the
   `X-Robots-Tag: noindex` header from your server config for production.

## 5. How to verify the fix worked

1. Recheck the page source / headers — `noindex` should be gone.
2. Google Search Console → URL Inspection → **Test Live URL** → confirm "Indexing allowed."
3. Click **Request Indexing** to speed up re-crawl.

## 6. Tools to double-check

- Google Search Console → URL Inspection & Page Indexing report
- Browser Dev Tools → Network tab (for header-based noindex)
