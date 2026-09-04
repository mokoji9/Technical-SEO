# Fix Guide: Missing Structured Data (Schema Markup)

**Category:** Structured Data

## 1. What's wrong

The page doesn't have structured data (schema markup) — a standardized code format that
explicitly tells search engines what the content is (an article, a product, a recipe, an
FAQ, a local business, etc.).

## 2. Why it matters

Structured data doesn't directly boost rankings, but it makes you eligible for **rich
results** in search (star ratings, FAQ dropdowns, product pricing, breadcrumbs) which
significantly increase click-through rate — and it helps AI-driven search/answer engines
understand and cite your content correctly.

## 3. How to check it yourself

1. Run the page through the
   [Rich Results Test](https://search.google.com/test/rich-results).
2. If nothing is detected, or errors/warnings show up, that's the issue.
3. You can also view page source (Ctrl+U) and search for `application/ld+json` to see if
   any schema exists at all.

## 4. Step-by-step fix

1. Identify the right schema type for the page (see [schema.org](https://schema.org) or
   Google's supported list). Common ones:
   - Articles/blog posts → `Article` or `BlogPosting`
   - Products → `Product`
   - FAQs → `FAQPage`
   - Local business → `LocalBusiness`
   - Reviews → `Review` / `AggregateRating`
2. Add a JSON-LD script in the page's `<head>` (or before `</body>`). Example for an
   article:
   ```html
   <script type="application/ld+json">
   {
     "@context": "https://schema.org",
     "@type": "Article",
     "headline": "Your Article Title",
     "author": {
       "@type": "Person",
       "name": "Author Name"
     },
     "datePublished": "2026-09-04",
     "image": "https://yourdomain.com/image.jpg"
   }
   </script>
   ```
3. Make sure every field matches what's **actually visible on the page** — Google penalizes
   markup that doesn't match visible content.
4. If using WordPress, plugins like Yoast/Rank Math can generate a lot of this
   automatically — check their schema settings before hand-coding.

## 5. How to verify the fix worked

1. Re-run the [Rich Results Test](https://search.google.com/test/rich-results) — confirm
   the schema type is detected with no errors.
2. Check Google Search Console → **Enhancements** section over the following days/weeks to
   see if rich result eligibility is confirmed.

## 6. Tools to double-check

- [Google Rich Results Test](https://search.google.com/test/rich-results)
- [Schema Markup Validator](https://validator.schema.org/)
- Google Search Console → Enhancements reports
