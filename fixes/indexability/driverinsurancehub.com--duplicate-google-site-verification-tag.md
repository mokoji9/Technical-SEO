# Fix Guide: Duplicate Google Search Console Verification Tag

**Category:** Indexability

## 1. What's wrong

The same `<meta name="google-site-verification">` tag appears twice in the page `<head>`, with
identical content on both. This usually means two separate integrations are both injecting their
own copy — commonly a theme setting/customizer field *and* an SEO plugin's verification field
both pointing at the same Search Console property.

## 2. Why it matters

- On its own this doesn't break verification or indexing — Google just reads the first instance
  and ignores the duplicate. But it's a sign of overlapping configuration between two places
  (theme + plugin, or two plugins), and the next person to touch site verification won't know
  which copy is the "real" one to update if the property ever changes.
- It's a small, free cleanup that removes a source of future confusion for no risk.

## 3. How to check it yourself

1. View source (`Ctrl+U`) on the homepage and search for `google-site-verification` — if it
   appears more than once, that's the duplicate.

## 4. Step-by-step fix (WordPress)

1. Check **Yoast SEO → Settings → Site features → General → Webmaster tools** (or search
   `google-site-verification` in the Yoast settings) for a verification code entered there.
2. Check **Appearance → Customize** for a theme-level "Header/Footer Scripts" or "Site
   Verification" field (Astra and similar themes sometimes offer this directly).
3. Also check any installed SEO/analytics plugin (e.g. Site Kit by Google, All in One SEO) for
   its own verification field — it's common for two of these to be configured at once after a
   plugin migration.
4. Keep exactly one copy — the simplest source of truth is usually
   **Google Search Console → Settings → Ownership verification → HTML tag**, kept in whichever
   single plugin/theme field is actually being used, and remove the tag from the other location.

## 5. How to verify the fix worked

1. View source again and confirm only one `google-site-verification` meta tag remains.
2. In Google Search Console, confirm the property still shows as verified (removing the
   *duplicate* copy, while leaving one identical tag in place, does not affect verification).

## 6. Tools to double-check

- View Page Source / Chrome Dev Tools → Elements
- [Google Search Console](https://search.google.com/search-console) → Settings → Ownership verification
