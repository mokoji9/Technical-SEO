# Fix Guide: Render-Blocking CSS/JavaScript

**Category:** Performance

## 1. What's wrong

CSS or JavaScript files are loading in a way that forces the browser to stop and wait
before it can show any content on screen — delaying the page from appearing, even if the
content itself is ready.

## 2. Why it matters

This directly hurts your LCP (Largest Contentful Paint) score and makes the site *feel*
slow, even on fast connections — a bad user experience and a ranking factor.

## 3. How to check it yourself

1. Run [PageSpeed Insights](https://pagespeed.web.dev/) on the page.
2. Look for "Eliminate render-blocking resources" in the diagnostics.
3. It will list the specific CSS/JS files causing the delay.

## 4. Step-by-step fix

1. **Defer non-critical JavaScript** — add `defer` (runs after HTML is parsed) so it doesn't
   block rendering:
   ```html
   <script src="script.js" defer></script>
   ```
2. **For scripts that must load early but don't depend on page order**, use `async`:
   ```html
   <script src="analytics.js" async></script>
   ```
3. **Inline critical CSS** (the minimum CSS needed for above-the-fold content) directly in
   the `<head>`, and load the rest of the stylesheet asynchronously:
   ```html
   <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
   ```
4. **Remove unused CSS/JS** — many CMS themes/plugins load libraries on every page even when
   unused. Audit and remove what isn't needed (Chrome Dev Tools → Coverage tab shows unused
   code).
5. **Combine/minify files** where possible to reduce the number of requests.

## 5. How to verify the fix worked

1. Re-run PageSpeed Insights — the "Eliminate render-blocking resources" warning should be
   gone or reduced.
2. Confirm LCP score has improved.
3. Manually check the page still looks and functions correctly (deferred scripts can
   sometimes break functionality if load order matters — test thoroughly).

## 6. Tools to double-check

- [PageSpeed Insights](https://pagespeed.web.dev/)
- Chrome Dev Tools → Lighthouse & Coverage tabs
- [WebPageTest](https://www.webpagetest.org/)
