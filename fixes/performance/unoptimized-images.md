# Fix Guide: Unoptimized Images Slowing Down the Site

**Category:** Performance

## 1. What's wrong

Images are too large in file size, not compressed, in outdated formats (JPEG/PNG instead of
WebP/AVIF), or missing size attributes — slowing down page load and hurting Core Web Vitals
(especially LCP and CLS).

## 2. Why it matters

Slow-loading pages rank worse and lose visitors before the page even finishes loading.
Google uses Core Web Vitals as a ranking factor, and images are usually the biggest culprit.

## 3. How to check it yourself

1. Run the page through [PageSpeed Insights](https://pagespeed.web.dev/).
2. Look for flags like "Serve images in next-gen formats," "Properly size images," or
   "Efficiently encode images."
3. Check the LCP (Largest Contentful Paint) score — if it's a slow image, PageSpeed will
   usually point to it directly.

## 4. Step-by-step fix

1. **Compress images** before uploading — use a tool like Squoosh, TinyPNG, or ShortPixel.
2. **Convert to modern formats** (WebP or AVIF), which are significantly smaller than
   JPEG/PNG at the same quality:
   ```html
   <picture>
     <source srcset="photo.avif" type="image/avif">
     <source srcset="photo.webp" type="image/webp">
     <img src="photo.jpg" alt="Description of the image" width="800" height="600">
   </picture>
   ```
3. **Always set width and height attributes** (or CSS aspect-ratio) so the browser reserves
   space before the image loads — this prevents layout shift (CLS):
   ```html
   <img src="photo.webp" alt="Team photo" width="800" height="600">
   ```
4. **Lazy-load offscreen images** (anything below the fold):
   ```html
   <img src="photo.webp" alt="..." loading="lazy" width="800" height="600">
   ```
   (Don't lazy-load the main hero/LCP image — that one should load immediately.)
5. **Use a CDN or image optimization service** if your platform supports it (Cloudflare
   Images, Shopify's built-in CDN, WordPress plugins like ShortPixel/Imagify).

## 5. How to verify the fix worked

1. Re-run [PageSpeed Insights](https://pagespeed.web.dev/) — confirm the image-related
   warnings are gone and LCP/CLS scores improved.
2. Check total page weight has dropped (Dev Tools → Network tab → check total transferred
   size).

## 6. Tools to double-check

- [PageSpeed Insights](https://pagespeed.web.dev/)
- [Squoosh](https://squoosh.app/) (manual compression/conversion)
- Chrome Dev Tools → Lighthouse tab
