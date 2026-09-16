# Checklist: Accessibility

Accessibility gaps often double as SEO/UX problems (screen readers and search crawlers both
rely on clean semantics), so check these alongside the other categories rather than skipping
them as "not SEO."

- [ ] Text/background color contrast meets WCAG AA (4.5:1 for body text, 3:1 for large text)
- [ ] All meaningful images have descriptive `alt` text (decorative images use `alt=""`)
- [ ] Embeds (video, audio, iframes) have accessible labels/titles, not just a generic name
- [ ] Heading structure is logical and sequential (one `<h1>`, no skipped levels)
- [ ] Forms have associated `<label>` elements, not placeholder text used as a label
- [ ] Interactive elements (buttons, links, menus) are reachable and operable via keyboard only
- [ ] Focus states are visible (no `outline: none` without a replacement focus style)
- [ ] Links have descriptive text (not bare "click here" / "read more" with no context)
- [ ] Site passes an automated scan (axe, Lighthouse Accessibility, WAVE) with no critical errors

**Related fix guides:** `fixes/accessibility/`
