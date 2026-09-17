# Fix Guide: Missing Favicon

**Category:** Site Architecture

## 1. What's wrong

The site has no favicon. Checking the rendered page for `<link rel="icon">` (or any `rel*="icon"`
variant) returns nothing, and DataForSEO's on-page check flags `no_favicon: true` on every page
checked (homepage, Colorado, Chicago, and Texas guide pages), confirmed again on this run.

## 2. Why it matters

- Google Search shows the favicon next to the site's result on both desktop and mobile — without
  one, Google falls back to a generic placeholder globe icon, which makes the result look less
  established/trustworthy next to competitors that do have a real icon.
- Browser tabs and bookmarks show a blank/default page icon instead of the brand mark, which
  hurts recognizability for anyone with multiple tabs open or who's bookmarked the site.
- It's a five-minute fix with no downside — there's no reason for a live site not to have one.

## 3. How to check it yourself

1. Visit `https://driverinsurancehub.com/favicon.ico` directly — a 404 means there's no fallback
   favicon at the default path either.
2. View source (`Ctrl+U`) and search for `rel="icon"` or `rel="shortcut icon"` in the `<head>` —
   if nothing matches, there's no favicon declared.
3. Look at the browser tab while the site is open — it'll show a generic blank/globe icon instead
   of a brand mark.

## 4. Step-by-step fix (WordPress + Astra theme)

1. In the WordPress admin, go to **Appearance → Customize → Site Identity**.
2. Upload a **Site Icon** — a square image, ideally 512×512px (WordPress will scale it down for
   browser tabs, mobile home-screen icons, etc.). A simplified version of the logo mark works
   better than the full logo-plus-wordmark at small sizes.
3. Save and publish. WordPress automatically outputs the correct `<link rel="icon">` tags across
   the site — no manual HTML editing needed on an Astra/WordPress build like this one.
4. If no square icon asset exists yet, crop the existing logo mark to a square canvas first
   (favicon generators like [RealFaviconGenerator](https://realfavicongenerator.net/) can also
   produce a full icon set — ICO, PNG sizes, Apple touch icon — from one source image).

## 5. How to verify the fix worked

1. Re-view page source and confirm `<link rel="icon" ...>` is present in the `<head>`.
2. Hard-refresh (`Ctrl+Shift+R`) and confirm the browser tab now shows the icon instead of the
   default placeholder.
3. Re-check `https://driverinsurancehub.com/favicon.ico` — it should now resolve instead of 404.

## 6. Tools to double-check

- Browser tab (visual check after a hard refresh)
- [RealFaviconGenerator](https://realfavicongenerator.net/) — checks an existing favicon setup
  across browsers/devices, or generates a full icon set from one image
- View Page Source / Chrome Dev Tools → Elements
