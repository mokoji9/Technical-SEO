# Fix Guide: No Focus Keyphrase Set on Any Page or Post

**Category:** Indexability

## 1. What's wrong

Every single piece of published content on the site — **all 94 pages and all 449 posts (543 of
543, 100%)** — has no Yoast SEO "Focus keyphrase" set. WordPress admin → Pages/Posts → the SEO
Score filter dropdown has a dedicated "SEO: No Focus Keyphrase" option, and selecting it returns
the full, unfiltered item count both times: nothing has ever had one set.

## 2. Why it matters

To be precise about what this is and isn't: **the focus keyphrase field itself is not read by
Google** — it's a Yoast-only field that doesn't appear anywhere in the page's HTML or affect
rankings directly. So this isn't a "Google can't find your keyword" problem.

What it actually does is power Yoast's on-page analysis checklist for whoever is writing the
content — it's what makes Yoast check things like "does your title contain the keyphrase," "is
there a meta description," "is the keyphrase in the first paragraph," and show a
traffic-light-style pass/fail list while writing. With no keyphrase set, that entire checklist
has nothing to check against and shows nothing actionable.

This lines up directly with the other findings in this audit: 614 pages missing a meta
description, 273 with an overly long title. Those aren't 543 separate authoring mistakes — they're
what happens when the one tool that would have caught them, page by page, as they were written,
was never actually engaged. This is very likely the root process gap behind those other findings,
not an isolated issue on its own.

## 3. How to check it yourself

1. WordPress admin → **Pages** (or **Posts**) → the **SEO Score** column filter dropdown above
   the list → select **"SEO: No Focus Keyphrase."**
2. The item count shown after filtering is how many have none set — compare it to "All" to see
   the proportion (on this site, filtered count = total count for both Pages and Posts).
3. Open any individual page/post → the Yoast SEO panel (click the Yoast icon in the editor
   toolbar) → **Focus keyphrase** field — confirm it reads the empty "Type here" placeholder.

## 4. Step-by-step fix

1. **Set a focus keyphrase on new content going forward, before publishing** — make this a
   required step in whatever publishing checklist/process is used, not optional.
2. **Go back through existing content, prioritized by real traffic potential** — use Google
   Search Console → Performance to find which pages already get impressions/clicks, and start
   there rather than working alphabetically through 543 items.
3. **Pick the keyphrase to match what someone would actually type into Google**, not just repeat
   the page title verbatim — usually the state/city + "rideshare insurance" pattern this site
   already uses in its URLs and headings.
4. **Once a keyphrase is set, actually act on what Yoast's checklist then shows** for that page —
   setting the field alone doesn't fix a meta description or title; it's what makes the tool start
   flagging those so they get fixed as part of the same pass.
5. **For a large backlog like this**, treat it as an ongoing part of the meta-description and
   title-length fixes already in this audit — doing all three together per page is more efficient
   than three separate passes through 543 items.

## 5. How to verify the fix worked

1. Re-check the "SEO: No Focus Keyphrase" filter in Pages/Posts — the count should drop as pages
   are updated.
2. Open a fixed page's Yoast panel and confirm the Focus keyphrase field is filled in and Yoast's
   analysis checklist is now showing real pass/fail feedback instead of nothing.

## 6. Tools to double-check

- WordPress admin → Pages/Posts → SEO Score filter → "SEO: No Focus Keyphrase"
- Yoast SEO panel in the block editor (per-page/post)

## 7. Suggested rewritten content

Example focus keyphrases for a few real pages — the pattern to repeat across the rest is
`{state or city} rideshare insurance` for the templated guide pages, or the specific service/topic
phrase for standalone pages:

- **Page:** Homepage
- **Current:** (none set)
- **Suggested keyphrase:** `rideshare insurance guide`

- **Page:** `/alabama-rideshare-insurance-for-uber-lyft-drivers/`
- **Current:** (none set)
- **Suggested keyphrase:** `Alabama rideshare insurance`

- **Page:** `/chicago-rideshare-insurance-for-uber-lyft-drivers/`
- **Current:** (none set)
- **Suggested keyphrase:** `rideshare insurance Chicago`

- **Page:** `/texas-rideshare-insurance/`
- **Current:** (none set)
- **Suggested keyphrase:** `Texas rideshare insurance`
