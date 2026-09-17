# Fix Guide: Overly Long Page Titles

**Category:** Indexability

## 1. What's wrong

Several pages have `<title>` tags well past Google's effective display limit. For example,
`/ai-liability/` uses:

> "AI Liability: Who Is Responsible When Artificial Intelligence Causes Harm? - AI Liability Guide"

That's 95 characters. Google typically truncates titles in search results at roughly 50-60
characters (varies by pixel width, not a hard character count), and this site's title pattern —
a long, full-sentence headline followed by " - AI Liability Guide" — pushes almost every
pillar/article page past that limit.

## 2. Why it matters

- A truncated title in the search results snippet ("AI Liability: Who Is Responsible When
  Artificial Intelligence Causes Ha…") looks unfinished and cuts off before the reader sees
  what the page actually answers, which hurts click-through rate.
- The site name suffix (" - AI Liability Guide") is often the part that gets cut, losing the
  brand recognition it was meant to add.
- Google may also rewrite the `<title>` entirely in the results snippet when it decides the
  original is a poor fit for the query — long, redundant titles make that rewrite more likely,
  which means you lose control over how the page is presented in search.

## 3. How to check it yourself

1. View source (`Ctrl+U`) on any page and find the `<title>` tag; count the characters.
2. Or run the page through a SERP snippet preview tool, e.g.
   [Portent's SERP Preview Tool](https://www.portent.com/serp-preview-tool), which shows
   exactly where Google would cut it off.
3. In this audit, DataForSEO's on-page check flagged `title_too_long: true` on
   `/ai-liability/` (95 characters) — the same title pattern likely repeats across the other
   pillar and article pages, so it's worth spot-checking a few more.

## 4. Step-by-step fix (WordPress + Yoast SEO)

1. In the WordPress admin, open the page/post (e.g. **Pages → AI Liability**).
2. Scroll to the **Yoast SEO** meta box below the editor and open the **Google preview** /
   **SEO** tab.
3. Yoast is currently auto-generating the title from the H1 plus the site name template. Click
   **Edit snippet** and write a shorter, purpose-built SEO title instead of reusing the full H1,
   e.g.:
   ```
   AI Liability: Who's Responsible? | AI Liability Guide
   ```
   (54 characters — keeps the core keyword phrase and the brand, drops the rhetorical
   "When Artificial Intelligence Causes Harm?" tail, which the H1 can keep in full.)
4. Repeat for other pillar/topic pages using the same long-headline-as-title pattern. Aim for
   ≤60 characters including the " | AI Liability Guide" suffix.
5. If most titles share this problem, consider adjusting Yoast's global title template under
   **Yoast SEO → Settings → Content types** so new pages default to a shorter pattern, rather
   than fixing every page one-by-one going forward.

## 5. How to verify the fix worked

1. View source again and confirm the `<title>` tag is under ~60 characters.
2. Re-run the page through the SERP preview tool and confirm it no longer shows a truncation
   ellipsis.
3. In Google Search Console → **Search appearance**, spot-check the page's search snippet after
   Google re-crawls it (can take days to weeks to reflect in live search results).

## 6. Tools to double-check

- [Portent's SERP Preview Tool](https://www.portent.com/serp-preview-tool)
- Yoast SEO's built-in snippet preview (shows a red/orange/green length indicator)
- Google Search Console → Search appearance
