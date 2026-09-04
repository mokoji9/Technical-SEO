# Checklist: Indexability

Can search engines index the pages once crawled — and are the *right* pages being indexed?

- [ ] No important pages have a `noindex` meta tag or `X-Robots-Tag: noindex` header by mistake
- [ ] Canonical tags exist on every page and point to the correct URL
- [ ] No canonical chains or conflicting canonicals
- [ ] No duplicate content across multiple URLs (www vs non-www, http vs https, trailing slash, params)
- [ ] Google Search Console "Page Indexing" report shows no unexpected exclusions
- [ ] Thin/low-value pages (tag pages, empty search results) are noindexed or consolidated
- [ ] Paginated series use correct canonical/self-referencing setup
- [ ] Soft 404s are identified and fixed (page returns 200 but shows "not found" content)
- [ ] Parameter handling is configured (GSC or robots.txt) for tracking/filter URLs

**Related fix guides:** `fixes/indexability/`
