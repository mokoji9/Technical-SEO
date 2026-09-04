# Fix Guide: Sitemap File Times Out / Returns a Server Error

**Category:** Crawlability

## 1. What's wrong

Your main sitemap index file loads fine, but one or more of the individual sitemap files it
points to don't. Instead of returning the XML list of URLs, the server hangs and eventually
returns a timeout or a `500 Internal Server Error` (LiteSpeed servers show this as a
"Request Timeout ... Connection Timeout" page). This is different from a sitemap that's simply
missing (404) — the file exists and is referenced correctly, but the server can't generate or
serve it in time.

## 2. Why it matters

Search engines fetch each sitemap file listed in your sitemap index to discover and re-check
your pages. If a specific sitemap file consistently times out, the crawler gives up on it —
meaning every page listed only in that file gets discovered solely through internal links
(slower) or not at all. Google Search Console will typically show that sitemap as "Couldn't
fetch" and stop retrying it as often. If the broken file covers your core pages (as opposed to
just blog posts), this is often the difference between new/updated pages showing up in Search
Console's "not indexed" list.

## 3. How to check it yourself

1. Open your sitemap index (usually `https://yourdomain.com/sitemap_index.xml`) and note every
   individual sitemap URL listed inside it.
2. Visit each one directly in a browser. A working sitemap shows XML with a list of `<loc>`
   entries almost instantly. A broken one will spin for 20-30+ seconds and then show an error
   page (or the browser tab will just say the connection timed out).
3. Confirm with `curl` from a terminal:
   ```
   curl -o /dev/null -w "Status: %{http_code}  Time: %{time_total}s\n" --max-time 30 https://yourdomain.com/the-sitemap-file.xml
   ```
   `Status: 000` with `Time: 30s` means it never got a response at all — a hang, not a normal
   error.
4. Check Google Search Console → **Sitemaps** report — a broken sub-sitemap usually shows
   "Couldn't fetch" or a red error status next to it.

## 4. Step-by-step fix

This is a server/hosting-side problem, not something you can fix by editing sitemap XML
directly — the file is being generated dynamically (typically by an SEO plugin like Rank Math
or Yoast) and something in that generation process is hanging. Work through these in order:

1. **Check how many URLs that specific sitemap is trying to list.** If it's WordPress pages
   (not posts), open **Pages → All Pages** and sort by date — an unusually large number of
   pages, or a handful of very heavy pages (huge amounts of content, many shortcodes, or an
   Elementor/Divi/Beaver Builder page with a very large layout) can cause the sitemap generator
   to time out building the entry for it.
2. **Temporarily disable caching/optimization plugins for sitemap URLs** (e.g. WP Rocket,
   LiteSpeed Cache) — some caching plugins interfere with dynamically-generated XML endpoints.
   In WP Rocket: **Settings → Cache** and check whether XML sitemaps are excluded from any
   "delay" or "lazy" features; in LiteSpeed Cache: check the **Exclude** settings for cache/
   optimization on `*sitemap*.xml`.
3. **Increase the PHP execution time limit / LiteSpeed connection timeout.** Ask your host
   (or, on Hostinger's hPanel, check **Advanced → PHP Configuration**) to raise `max_execution_time`
   and the LiteSpeed "Connection Timeout" — if the sitemap generator just needs a few more
   seconds, this alone can fix it.
4. **Regenerate the sitemap.** In Rank Math: **Rank Math → Sitemap Settings**, toggle sitemaps
   off and back on to force a fresh rebuild. In Yoast: **SEO → General → Features → toggle XML
   sitemaps off/on**.
5. **Check the server error log** (via hosting panel → Error Logs, or ask your host) for the
   exact PHP error/timeout at the moment you request the broken sitemap URL — this will point
   directly at the plugin or query causing it.
6. If none of the above resolves it, ask your host to check for a resource limit being hit
   (memory limit, CPU throttling) specifically on that URL — shared hosting plans sometimes
   throttle processes that run too long, which looks identical to a hang from the outside.

## 5. How to verify the fix worked

1. Re-run the `curl` command from step 3 above — it should return `Status: 200` in well under
   5 seconds, with real XML content (not an error page).
2. Open the file in a browser and confirm it lists real `<loc>` URLs.
3. In Google Search Console → **Sitemaps**, click into the sitemap and confirm it shows
   "Success" with a URL count, not "Couldn't fetch."
4. Spot-check a few of the URLs listed in it to confirm they return 200, not 404s.

## 6. Tools to double-check

- Google Search Console → Sitemaps report
- `curl -w "%{http_code} %{time_total}s\n"` from a terminal (see step 3)
- Your hosting panel's Error Log viewer (find the exact server-side error)
