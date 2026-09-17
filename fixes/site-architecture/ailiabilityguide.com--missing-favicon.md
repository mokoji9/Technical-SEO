# Fix Guide: Missing Favicon

**Category:** Site Architecture

## 1. What's wrong

The site has no favicon. Checking the rendered page for `<link rel="icon">` (or any
`rel*="icon"` variant) returns nothing, and DataForSEO's on-page check flags `no_favicon: true`
on every page crawled.

## 2. Why it matters

- Browser tabs, bookmarks, and history entries show a blank/generic icon instead of a
  recognizable brand mark, which makes the site harder to spot among a user's other open tabs.
- Google displays the favicon next to the site's listing in mobile search results — a missing
  one makes the result look less trustworthy/complete next to competitors who have one.
- It's flagged in Lighthouse's Best Practices/SEO checks as a small but easy completeness gap.

## 3. How to check it yourself

1. View source (`Ctrl+U`) and search for `rel="icon"` — if nothing appears, there's no favicon
   declared.
2. Visit `https://ailiabilityguide.com/favicon.ico` directly — if it 404s, no fallback favicon
   exists either.
3. Look at the browser tab while the site is open — it will show a generic blank page icon.

## 4. Step-by-step fix (WordPress)

1. Create a square image (512×512px recommended) using the site's logo/wordmark — since this
   site currently uses a text wordmark rather than a logo image, a simple monogram (e.g. a
   stylized "AI" or "⚖" scale icon fitting the legal/compliance theme) works well as a starting
   point.
2. In the WordPress admin, go to **Appearance → Customize → Site Identity** (or
   **Settings → General** on newer WordPress versions with full-site editing).
3. Upload the image under **Site Icon**. WordPress automatically generates the necessary
   `<link rel="icon">` tags and multiple sizes (including the Apple touch icon) — no theme code
   edit needed.
4. Save/publish the change.

## 5. How to verify the fix worked

1. View source again and confirm `<link rel="icon" ...>` tags now appear in the `<head>`.
2. Hard-refresh the site in a browser (favicons are aggressively cached) and confirm the tab
   icon shows the new image.
3. Re-run the DataForSEO/Lighthouse on-page check and confirm `no_favicon` no longer flags.

## 6. Tools to double-check

- Browser tab (hard refresh / incognito window to bypass favicon caching)
- [realfavicongenerator.net](https://realfavicongenerator.net/) — generates all icon sizes/
  formats from one source image if broader device coverage is wanted later
