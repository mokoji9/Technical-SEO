# Fix Guide: Pages with Only One Incoming Internal Link

**Category:** Site Architecture

## 1. What's wrong

Ahrefs Site Audit found 16 indexable pages (and 9 more non-indexable ones) that have only **one**
dofollow incoming internal link — the bare minimum to be reachable at all, one broken or removed
link away from becoming a true orphan. Ahrefs also flagged that its crawl hit maximum depth
before finishing, and the site's HTTP-status-by-depth chart shows a long tail of pages sitting
9+ clicks from the homepage.

## 2. Why it matters

Internal links are one of the main signals search engines use to judge how important a page is
and how often to recrawl it. A page reachable by only one link — especially if that link is
buried several clicks deep — sends a weak priority signal, similar in kind (if less extreme) to a
true orphan page. This lines up with what Google Search Console shows for this domain: 151 pages
"Discovered - currently not indexed" and 20 "Crawled - currently not indexed" — 171 pages Google
knows about via the sitemap but hasn't prioritized. Thin internal linking across a large content
set (184 pages/posts) is a plausible structural contributor to that gap.

## 3. How to check it yourself

1. Ahrefs Site Audit → Links → "Page has only one dofollow incoming internal link" — lists the
   affected URLs.
2. Ahrefs Site Audit → Overview → "HTTP status codes by depth level" chart — look for pages
   clustering at high depth (6+ clicks from the homepage).
3. Cross-check a flagged URL against Search Console → Indexing → Pages → "Discovered" or
   "Crawled — currently not indexed."

## 4. Step-by-step fix

1. **Export the flagged URLs** from Ahrefs.
2. **Add each to a second, real navigation path** — a topic hub page listing all posts under
   that pillar, a "related articles" module at the bottom of pillar pages, or a cross-link from
   a closely related post.
3. **Reduce click depth where possible** — if a post is 8-9 clicks from the homepage, consider
   whether a category/hub page one or two levels up should link to it directly instead of relying
   on pagination alone.
4. **Prioritize by real search demand** using GSC → Performance, so pages already earning
   impressions get a stronger internal-linking push first.

## 5. How to verify the fix worked

1. Re-run Ahrefs Site Audit and confirm the "only one incoming internal link" count has dropped.
2. Re-check the depth-distribution chart for fewer pages at high depth.
3. Watch GSC's "Discovered/Crawled — not indexed" counts over the following weeks for a decline.

## 6. Tools to double-check

- Ahrefs Site Audit → Links, and the Overview depth chart
- Google Search Console → Indexing → Pages
- [Screaming Frog SEO Spider](https://www.screamingfrog.co.uk/seo-spider/) — visualizes crawl
  depth and internal link count per URL
