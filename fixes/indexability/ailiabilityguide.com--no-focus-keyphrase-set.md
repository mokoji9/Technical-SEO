# Fix Guide: No Focus Keyphrase Set on Any Page or Post

**Category:** Indexability

## 1. What's wrong

Every single piece of published content on the site — **all 18 pages and all 166 posts (184 of
184, 100%)** — has no Yoast SEO "Focus keyphrase" set. WordPress admin → Pages/Posts → the SEO
Score filter dropdown has a dedicated "SEO: No Focus Keyphrase" option, and selecting it returns
the full, unfiltered item count both times: nothing has ever had one set.

This is the same pattern found on driverinsurancehub.com (a different site run through this same
workflow) — worth knowing if these sites share an operator/template setup, since it points to a
process gap rather than a one-off oversight.

## 2. Why it matters

To be precise about what this is and isn't: **the focus keyphrase field itself is not read by
Google** — it doesn't appear in the page's HTML or affect rankings directly. What it actually
does is power Yoast's on-page checklist for whoever is writing the content (does the title
contain the keyphrase, is there a meta description, is the keyphrase used naturally in the body).
With it never set, that checklist has never actually triggered for any of the 184 pieces of
content — which plausibly explains why the meta-description and title-length gaps found
elsewhere in this audit exist on a real (if partial) share of pages rather than nowhere: the tool
that would nudge a writer to fix them per-page was never engaged.

## 3. How to check it yourself

1. WordPress admin → **Pages** (or **Posts**) → the **SEO Score** column filter dropdown above
   the list → select **"SEO: No Focus Keyphrase."**
2. Compare the filtered item count to "All" — on this site, filtered count = total count for
   both Pages and Posts.
3. Open any individual page/post → the Yoast SEO panel (click the Yoast icon in the editor
   toolbar) → **Focus keyphrase** field — confirm it reads the empty "Type here" placeholder.

## 4. Step-by-step fix

1. **Set a focus keyphrase on new content going forward, before publishing** — make it a required
   step in the publishing checklist.
2. **Go back through existing content, prioritized by real traffic potential** — use Google
   Search Console → Performance to find which pages already get impressions/clicks.
3. **Pick a keyphrase that matches how someone would actually search**, not just the page title
   verbatim — this site's own topic pillars (AI governance, AI liability, AI compliance, etc.)
   already suggest natural phrases.
4. **Once set, act on what Yoast's checklist then shows** for that page — the field alone doesn't
   fix a missing description or long title; it's what makes the tool start flagging those.

## 5. How to verify the fix worked

1. Re-check the "SEO: No Focus Keyphrase" filter in Pages/Posts — the count should drop.
2. Open a fixed page's Yoast panel and confirm the checklist now shows real pass/fail feedback.

## 6. Tools to double-check

- WordPress admin → Pages/Posts → SEO Score filter → "SEO: No Focus Keyphrase"
- Yoast SEO panel in the block editor (per-page/post)

## 7. Suggested rewritten content

Example focus keyphrases for the site's actual pillar pages — the pattern to repeat across the
remaining posts is the specific AI-governance sub-topic each one covers:

- **Page:** Homepage
- **Current:** (none set)
- **Suggested keyphrase:** `AI liability guide`

- **Page:** `/ai-liability/`
- **Current:** (none set)
- **Suggested keyphrase:** `AI liability`

- **Page:** `/ai-risk-insurance-organizations-manage-ai-liability/` (AI Risk & Insurance)
- **Current:** (none set)
- **Suggested keyphrase:** `AI liability insurance`

- **Page:** AI Regulation and Compliance pillar page
- **Current:** (none set)
- **Suggested keyphrase:** `AI regulatory compliance`
