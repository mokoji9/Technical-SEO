# Fix Guide: Missing or Broken XML Sitemap

**Category:** Crawlability

## 1. What's wrong

There's no XML sitemap (a file listing all the important pages on your site), or it exists
but is broken/outdated/not submitted to Google.

## 2. Why it matters

A sitemap helps search engines discover your pages faster, especially on large sites or
pages with few internal links pointing to them. Without one, new/updated pages can take
much longer to get crawled and indexed.

## 3. How to check it yourself

1. Visit `https://yourdomain.com/sitemap.xml`. If you get a 404, there's no sitemap (or it's
   at a different URL — check `robots.txt` for a `Sitemap:` line).
2. In Google Search Console → **Sitemaps**, check if one is submitted and whether it shows
   errors.

## 4. Step-by-step fix

**If using a CMS (WordPress, Shopify, Webflow, etc.):**
1. Most SEO plugins generate one automatically. In WordPress with Yoast: go to
   **Yoast SEO → General → Features** and make sure "XML sitemaps" is enabled.
2. Your sitemap will usually be at `/sitemap_index.xml` or `/sitemap.xml`.

**If building manually:**
1. Create an XML file listing your key pages:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
     <url>
       <loc>https://yourdomain.com/</loc>
       <lastmod>2026-09-04</lastmod>
     </url>
     <url>
       <loc>https://yourdomain.com/about/</loc>
       <lastmod>2026-09-04</lastmod>
     </url>
   </urlset>
   ```
2. Upload it to your site's root as `sitemap.xml`.
3. Add a reference in `robots.txt`:
   ```
   Sitemap: https://yourdomain.com/sitemap.xml
   ```

**Either way, then:**
4. Go to Google Search Console → **Sitemaps** → enter `sitemap.xml` → click **Submit**.
5. Do the same in Bing Webmaster Tools if you track Bing traffic.

## 5. How to verify the fix worked

1. Google Search Console → Sitemaps should show "Success" status with a URL count.
2. Spot-check a few URLs from the sitemap to confirm they return 200 (not 404 or redirects).

## 6. Tools to double-check

- Google Search Console → Sitemaps report
- Any "XML sitemap validator" tool online
