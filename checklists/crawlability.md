# Checklist: Crawlability

Can search engines actually reach and crawl your pages?

- [ ] `robots.txt` exists at `/robots.txt` and returns a 200 status
- [ ] `robots.txt` isn't accidentally blocking important pages (`Disallow: /`)
- [ ] `robots.txt` references the XML sitemap
- [ ] XML sitemap exists and is submitted in Google Search Console
- [ ] Sitemap only includes indexable, canonical, 200-status URLs
- [ ] Sitemap is under 50,000 URLs / 50MB (or properly split into a sitemap index)
- [ ] No important pages are orphaned (zero internal links pointing to them)
- [ ] Crawl budget isn't wasted on low-value pages (filters, duplicate params, infinite spaces)
- [ ] No crawl traps (infinite calendars, faceted navigation loops)
- [ ] Server responds quickly and consistently to crawler requests (no timeouts)
- [ ] No excessive redirect chains (A → B → C → D)

**Related fix guides:** `fixes/crawlability/`
