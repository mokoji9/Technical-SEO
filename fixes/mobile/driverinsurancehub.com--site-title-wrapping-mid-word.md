# Fix Guide: Site Title Wraps Mid-Word on Mobile

**Category:** Mobile

## 1. What's wrong

On mobile screens, the header's site title breaks across four lines mid-word: "Driver / Insura /
nce / Hub" instead of wrapping cleanly at word boundaries ("Driver / Insurance / Hub" or similar).
Inspecting the element (`.site-branding.ast-site-identity` — an Astra theme header component)
shows `overflow-wrap: anywhere` applied to it, inside a header column that's rendering narrower
than the text needs. `overflow-wrap: anywhere` tells the browser it's allowed to break a word at
any character once it runs out of room — normally a safety net for genuinely unbreakable strings
like long URLs, but here it's kicking in on an ordinary three-word site name because its
container is too narrow at this breakpoint.

## 2. Why it matters

- This renders on every single page load on mobile, before any real content — it's the very
  first thing a phone visitor sees, and it reads as broken/unpolished.
- It pushes the actual page content further down the screen, costing valuable above-the-fold
  space on the device most visitors are using (mobile-first indexing means Google evaluates this
  same mobile rendering when assessing the page).

## 3. How to check it yourself

1. Open the site on a phone, or in Chrome Dev Tools → toggle device toolbar (Ctrl+Shift+M) → set
   width to 375px.
2. Look at the header — if the site name breaks mid-word rather than wrapping at spaces, that's
   the bug.
3. In Dev Tools → Elements, select the site title element and check the Styles panel for
   `overflow-wrap: anywhere` (or `word-break: break-all`) plus the actual rendered width of its
   parent container.

## 4. Step-by-step fix (Astra theme)

1. In the WordPress admin, go to **Appearance → Customize → Header Builder** (Astra's header
   customizer).
2. Select the **Site Identity** element and check its **width settings** — Astra's header
   sometimes constrains the logo/title column to a fixed or percentage width that's too narrow
   once the header also has to fit a mobile menu icon next to it.
3. If a width constraint isn't the direct cause, add a small custom CSS override under
   **Appearance → Customize → Additional CSS** (loads sitewide, no plugin needed):
   ```css
   @media (max-width: 544px) {
     .site-branding.ast-site-identity,
     .ast-site-identity .site-title {
       overflow-wrap: normal;
       word-break: normal;
       max-width: none;
       white-space: normal;
     }
   }
   ```
4. If the title still feels cramped next to the mobile menu icon at very narrow widths, consider
   either shortening the displayed site name (Astra lets you set a shorter "Site Identity" text
   separate from the full site title) or reducing its font size slightly at the mobile breakpoint
   instead of fighting the wrap behavior.

## 5. How to verify the fix worked

1. Re-check at 375px (and 360px/390px/414px for good measure) in Dev Tools' device toolbar —
   confirm "Driver Insurance Hub" now wraps only at spaces, if it wraps at all.
2. Confirm the desktop header is unaffected by the change (the media query above only targets
   mobile widths).
3. Re-run [Google's Mobile-Friendly Test](https://search.google.com/test/mobile-friendly) on the
   homepage.

## 6. Tools to double-check

- Chrome Dev Tools → Device Toolbar (Ctrl+Shift+M), testing at 360px, 375px, 390px, 414px
- [Google's Mobile-Friendly Test](https://search.google.com/test/mobile-friendly)
- A real phone, if available
