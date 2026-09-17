# Fix Guide: Orphan Pages (No Incoming Internal Links)

**Category:** Site Architecture

## 1. What's wrong

Ahrefs Site Audit found **44 orphan pages** on driverinsurancehub.com — pages that exist and are
in the sitemap, but that no other page on the site links to. Google can still find them (via the
sitemap), but nothing on the site itself points to them.

## 2. Why it matters

- Internal links are one of the main signals search engines use to judge how important a page
  is and how often to recrawl it. A page with zero incoming internal links reads as low-priority,
  even if the content itself is good.
- This lines up directly with what Google Search Console shows for this domain: 315 pages
  "Discovered - currently not indexed" and 72 "Crawled - currently not indexed" — 387 pages
  Google knows about (from the sitemap) but hasn't prioritized crawling or indexing. Orphan pages
  are a common, concrete cause of exactly that pattern — being *in* the sitemap isn't enough to
  earn a crawl budget; being *linked to* is what signals a page is worth indexing.
- Real visitors browsing the site (not arriving from search or a direct link) can't reach these
  pages either — there's no path to them through normal navigation.

## 3. How to check it yourself

1. Ahrefs Site Audit → Content/Overview → "Orphan page (has no incoming internal links)" — lists
   every affected URL.
2. Manually: pick a page and check whether it appears in the main nav, the homepage's "Select
   Your State" list, any related-guides module, or another state/city page's body copy. If it's
   reachable only via a direct URL or the sitemap, it's orphaned.
3. Cross-check against Search Console → Indexing → Pages → "Discovered - currently not indexed" /
   "Crawled - currently not indexed" — a page appearing on both lists is a strong candidate for
   this exact cause.

## 4. Step-by-step fix

1. **Export the full list of 44 orphan URLs** from Ahrefs Site Audit.
2. **Add each one to at least one real navigation path.** For a state/city insurance-guide site
   like this, the natural fix is usually one (or more) of:
   - Add it to the homepage's "Select Your State" list if it's a state/city guide that's missing
     from that index.
   - Cross-link it from a related state page's body copy (e.g. neighboring states, or a city page
     linking to its state's page and vice versa).
   - Add a "Related guides" module at the bottom of each state/city page listing nearby states or
     related cities, generated from the CMS's existing taxonomy so it stays correct as pages are
     added.
3. **Prioritize by what's already getting search demand** — cross-reference against the GSC
   Performance report so pages already earning impressions get linked in first.
4. **Avoid creating a new orphan problem while fixing this one** — when adding links, make sure
   they're real `<a href>` links in the rendered HTML, not JavaScript-only interactions that a
   crawler won't follow.

## 5. How to verify the fix worked

1. Re-run Ahrefs Site Audit and confirm the "Orphan page" count has dropped to 0 (or is trending
   down as pages are linked in).
2. In Google Search Console → URL Inspection, test a few previously-orphaned URLs and confirm
   Google now shows them as discovered via a normal crawl path, not just the sitemap.
3. Watch the "Discovered - currently not indexed" / "Crawled - currently not indexed" counts in
   GSC → Indexing → Pages over the following weeks — they should decline as internal links give
   Google a reason to prioritize crawling these pages.

## 6. Tools to double-check

- Ahrefs Site Audit → Content (or Internal link opportunities)
- Google Search Console → Indexing → Pages, and URL Inspection
- [Screaming Frog SEO Spider](https://www.screamingfrog.co.uk/seo-spider/) — "Orphan Pages"
  report cross-references the sitemap against the crawl to find the same issue independently
