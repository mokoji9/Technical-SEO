# Fix Guide: Multiple `<h1>` Tags on One Page

**Category:** Site Architecture

## 1. What's wrong

A page has more than one `<h1>` heading. Headings are meant to form a single, logical outline of
a page — one `<h1>` stating what the page is about, then `<h2>`/`<h3>` etc. for its sections. When
a page has several `<h1>`s (often because a design element like a card, banner, or repeated
section title was styled using an `<h1>` tag purely for its visual size), that outline breaks.

## 2. Why it matters

Search engines use heading structure as one signal for understanding what a page is primarily
about and how its content is organized. A single, clear `<h1>` reinforces the page's main topic;
splitting that signal across 6-8 `<h1>`s (as with a homepage that gives equal top-level weight to
its main headline *and* every category/region card on the page) dilutes it and makes the page's
core topic less clear to both search engines and assistive technology (screen readers use
heading level to navigate a page, and expect exactly one `<h1>`).

## 3. How to check it yourself

1. View page source (Ctrl+U) and search for `<h1` — count how many appear.
2. Or, in Chrome Dev Tools → Console, run:
   ```js
   document.querySelectorAll('h1').forEach(el => console.log(el.textContent.trim()))
   ```
3. Free tools like the [SEO META in 1 CLICK](https://chromewebstore.google.com/) extension or
   [Screaming Frog](https://www.screamingfrog.co.uk/seo-spider/) will flag "Multiple H1 tags" as
   an issue directly.

## 4. Step-by-step fix

1. **Decide which single heading is the true `<h1>`** — usually the main page headline (e.g. the
   hero title), not a repeated card/section label.
2. **Change every other `<h1>` to the correct level** based on its actual place in the page
   outline — typically `<h3>` or `<h4>` for card titles inside a grid/section, `<h2>` for real
   section headings:
   ```html
   <!-- Before -->
   <h1>Oklahoma</h1>
   <h1>Georgia Mountains</h1>

   <!-- After -->
   <h3>Oklahoma</h3>
   <h3>Georgia Mountains</h3>
   ```
3. **In most page builders/CMS platforms** (Webflow, WordPress, Squarespace), the heading level
   is a dropdown/setting on the text element itself — no CSS changes are needed, since visual
   size is controlled separately from the semantic tag. Changing the tag does not have to change
   how the text looks.
4. **Re-scan the full page outline** afterward to confirm there's a clean hierarchy: one `<h1>`,
   then `<h2>`s for major sections, `<h3>`s nested under them, without skipping levels.

## 5. How to verify the fix worked

1. Re-run the console query or extension check from Step 3 — confirm exactly one `<h1>` remains.
2. Visually confirm the page looks identical (heading *level* changed, not its styling).
3. Re-check with an accessibility tool (see below) to confirm the heading outline now reads
   top-to-bottom without skipped levels.

## 6. Tools to double-check

- Chrome Dev Tools → Console (`document.querySelectorAll('h1')`)
- [WAVE Accessibility Evaluation Tool](https://wave.webaim.org/) — shows the full heading
  structure/outline for a page
- [Screaming Frog SEO Spider](https://www.screamingfrog.co.uk/seo-spider/) (free up to 500 URLs)
  — bulk-checks every page on the site for multiple/missing H1s at once
