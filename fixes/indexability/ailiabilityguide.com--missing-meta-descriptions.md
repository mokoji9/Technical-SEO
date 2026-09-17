# Fix Guide: Missing or Too-Long Meta Descriptions

**Category:** Indexability

## 1. What's wrong

The 2026-09-06 audit only sampled the homepage and `/ai-liability/`, and both happened to have a
real meta description — so this was missed. Ahrefs Site Audit's full crawl (351 internal URLs)
shows it's a real, sitewide issue on a meaningful share of *other* pages: **23 indexable pages
have no meta description at all**, another **16 non-indexable pages** are also missing one, and
**2 pages have a description that's too long**.

## 2. Why it matters

- Without a description, Google writes its own snippet by pulling text from wherever on the page
  it thinks best answers the query — usually a worse, less persuasive fragment than one written
  deliberately, and inconsistent from page to page.
- A too-long description gets truncated mid-sentence in the search snippet, which reads as
  unfinished.
- Since the homepage and flagship `/ai-liability/` page already have good, hand-written
  descriptions, this isn't a site-wide template problem — it's specific pages that were missed,
  which makes it worth an actual page-by-page pass rather than a template-level fix.

## 3. How to check it yourself

1. Ahrefs Site Audit → Content → Issues → "Meta description tag missing or empty" and "Meta
   description too long" — exports the exact affected URLs.
2. View source (`Ctrl+U`) on any flagged page and search for `name="description"` — confirm
   it's genuinely absent (not just empty) or count its characters if flagged as too long.

## 4. Step-by-step fix (WordPress + Yoast SEO)

1. Export the list of affected URLs from Ahrefs.
2. For each: open the page/post in WordPress, expand the Yoast SEO snippet editor, and write a
   real description (~120-155 characters) — see the drafted examples below for the pattern this
   site already uses on its working pages.
3. For the 2 too-long descriptions, trim to fit within Google's display limit without losing the
   core answer.

## 5. How to verify the fix worked

1. Re-run Ahrefs Site Audit and confirm both issue counts drop toward 0.
2. View source on a fixed page and confirm the description reads as a complete, real sentence.

## 6. Tools to double-check

- Ahrefs Site Audit → Content → Issues
- Yoast SEO's built-in snippet preview
- View Page Source / Chrome Dev Tools → Elements

## 7. Suggested rewritten content

The site's existing good descriptions (homepage: *"Your complete resource for AI liability,
governance, compliance, insurance, vendor risk, and legal guidance for organizations deploying
artificial intelligence."*; `/ai-liability/`: *"Learn who may be legally responsible when AI
systems cause harm, how liability is determined, and how organizations reduce legal and
regulatory risk."*) set the pattern to repeat: state what the page covers, then the practical
payoff for the reader (risk reduction, compliance readiness). Apply the same pattern to each
flagged page's actual topic — e.g. for a page titled "AI Vendor Risk and Third-Party Liability
Exposure," a description like *"How organizations assess and manage liability exposure from
third-party AI vendors, including contract terms, due diligence, and risk transfer."* follows the
same voice and length as the site's existing working examples.
