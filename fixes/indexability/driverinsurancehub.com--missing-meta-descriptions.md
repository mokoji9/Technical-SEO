# Fix Guide: Missing Meta Descriptions

**Category:** Indexability

## 1. What's wrong

Pages don't have a `<meta name="description">` tag at all — checked the homepage and an inner
content page, and both come back flagged `no_description`. Because there's no manual
description, Open Graph's `og:description` falls back to WordPress's auto-generated excerpt,
which visibly truncates mid-sentence with a literal bracket ellipsis: *"...requirements, coverage
gaps, and how […]"*.

## 2. Why it matters

- Without a meta description, Google writes its own snippet by pulling text from wherever on the
  page it thinks best answers the query — which is often an awkward mid-paragraph fragment
  instead of a clear, persuasive summary you control.
- The `[…]` artifact showing up in social share previews (Facebook, LinkedIn, Slack unfurls) looks
  broken/unfinished to anyone sharing a link, which is a small but real trust hit right at the
  point someone is deciding whether to click.
- Meta descriptions are one of the few pieces of a search snippet you fully control — leaving it
  blank is giving up free control over click-through rate for no benefit.

## 3. How to check it yourself

1. View source (`Ctrl+U`) on any page and search for `name="description"` — if it's missing
   entirely (not just empty), that's the issue.
2. Search Google for `site:driverinsurancehub.com` and look at the snippet text shown for each
   result — an auto-generated snippet often reads as a disjointed sentence fragment.
3. Paste a page URL into the [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/)
   and check whether the preview description ends in a stray `[…]`.

## 4. Step-by-step fix (WordPress + Yoast SEO)

1. Open a page/post in the WordPress admin and scroll to the **Yoast SEO** meta box.
2. Open the **Google preview** / snippet editor and click **Edit snippet**.
3. Write a real, hand-crafted meta description (~120-155 characters) that summarizes the page and
   gives a reason to click, e.g. for the homepage:
   ```
   State-by-state rideshare insurance guides for Uber and Lyft drivers — coverage gaps,
   costs, and how to choose the right policy.
   ```
4. Repeat for the state-guide template pages — since every state page follows the same structure,
   consider setting a Yoast **content type template** under **Yoast SEO → Settings → Content
   types → Pages/Posts** so new pages get a sensible default description automatically (still
   worth hand-writing the description for the highest-traffic pages individually).
5. Because there are ~50 state pages on the same template, prioritize the homepage and the
   highest-traffic states first, then work through the rest.

## 5. How to verify the fix worked

1. View source again and confirm `<meta name="description" content="...">` is present with real
   text (not empty, not auto-truncated).
2. Re-check the Facebook Sharing Debugger / Twitter Card Validator and confirm the preview
   description reads as a complete sentence, not one ending in `[…]`.
3. In Google Search Console → Performance, monitor click-through rate on fixed pages over the
   following weeks.

## 6. Tools to double-check

- View Page Source / Chrome Dev Tools → Elements
- [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/)
- Yoast SEO's built-in snippet preview
