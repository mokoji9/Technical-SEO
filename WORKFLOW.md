# Technical SEO Workflow

This is the process to follow every time we audit a website and fix issues.
Written for beginners — no assumed SEO background.

## Step 0 — Ask: Automated or Manual?

Every time an audit starts, always ask:

> "Do you want me to pull data automatically using connected SEO tools, or will you provide the data yourself (crawl export, Search Console, PageSpeed report, etc.)?"

- If **automated**: use available tools (Semrush, DataForSEO, site audit/crawl skills) to gather crawl data, performance data, backlinks, indexation status — **and** check the user's own connected accounts for the domain, using Claude in Chrome (the user's real, logged-in browser, not the sandboxed preview browser).

  **Before checking GSC/Ahrefs/the CMS admin, confirm the right browser is actually connected** — this catches a connection problem upfront instead of mid-audit:
  1. Call `list_connected_browsers`, then navigate it to one target dashboard (GSC is a good test). Signed-in view → connected correctly, proceed.
  2. Logged-out/marketing page → wrong profile is connected. Walk through, in order, stopping as soon as it works: (a) ask which Chrome profile the user is actually logged into these accounts in; (b) in that profile, confirm the Claude in Chrome extension is installed and enabled (`chrome://extensions`); (c) have them click the extension's own icon there and confirm it's signed into the same Claude account as this session — installed isn't enough, it must be open and signed in; (d) call `switch_browser` and have them watch for a "Connect" prompt in that profile; (e) if that still doesn't work, have them **fully quit Chrome** (every window/profile, not just tabs) and reopen directly into that one profile only, then retry `switch_browser` — a stale connection to the wrong profile is usually what's blocking the new one.
  3. Still not connecting after that → stop retrying, fall back to the user relaying the key screens/data manually, and note that in the audit.

  Once connected, check:
  - **Google Search Console** — Coverage/Page Indexing status, Core Web Vitals (field data), Sitemaps status, Manual Actions/Security Issues, for the matching property.
  - **Ahrefs** (or whichever rank/backlink tool is logged in) — Site Audit health score, organic keyword rankings, backlink profile.
  - **The site's own CMS admin, if logged in** (WordPress + Yoast/RankMath, Shopify, Webflow, etc.) — check its bulk SEO-health views, not just individual pages. On WordPress + Yoast, for example, the Pages/Posts list has an "SEO Score" column and filter with a "No Focus Keyphrase" option — filtering by it gives an exact sitewide count in one step, and often surfaces the *process* reason behind on-page findings (the plugin's checklist never having triggered for any content usually explains why a missing-meta-description or overly-long-title finding is sitewide rather than isolated).
  - Anything else already logged in and clearly relevant (Bing Webmaster Tools). Don't hunt through unrelated accounts.

  If GSC/Ahrefs/the CMS admin aren't logged in, the site isn't added there, or Claude in Chrome isn't available, say so and continue with the other tools — note what was skipped so the audit isn't presented as more complete than it is. Never state a number from one of these dashboards from memory or infer it from crawl data — if you didn't actually see it there, call it unverified.
- If **manual**: ask what data the user has (e.g. a Screaming Frog CSV, Google Search Console export, PageSpeed Insights report, robots.txt/sitemap URLs) and analyze what's provided.

Never assume — always confirm which mode for that specific audit.

## Step 1 — Scope the audit

Decide (or ask) what's being audited:
- Whole site or specific section/pages?
- Which categories matter most right now? (see `checklists/`)

## Step 2 — Run the audit

Go through the relevant checklist(s) in `checklists/` and record findings.

## Step 3 — Create the audit folder

Create `audits/{site-name}-{YYYY-MM-DD}/` containing:
- `findings.md` — raw list of everything found (use `templates/audit-report-template.md`)
- `issue-tracker.md` — prioritized list (use `templates/issue-tracker-template.md`)

## Step 3b — Build the designed HTML report (always, not optional)

Every audit ends with a polished HTML report in the audit folder as `report.html`, published
as a Claude Artifact. Do this automatically as part of Step 3 — don't wait to be asked and
don't offer it as an extra. An audit that stops at the markdown files is unfinished.

Start from `templates/report-template.html` — it has the full design system (light/dark
theming, severity color-coding, stat tiles, finding cards, per-finding step-by-step fix
blocks) already built. Read the comment block at the top of that file first: it explains what
must be rebuilt per audit (the site's real accent color and logo, all copy and findings) versus
what's safe to reuse as-is (the CSS structure). Load the `artifact-design` skill before
starting.

The report must include, for every finding, a **"How to fix it, step by step"** block: numbered
steps written for that specific site (name the actual CMS, plugins, and admin screens where
known), a code snippet where one applies, and a one-line "Done when" verification. Pull the
steps from the matching guide in `fixes/` and tailor them — don't paste the generic guide.

The template's stat cards include a real score bar (width = the actual 0-100 Lighthouse score)
and, for Core Web Vitals, a qualitative label set from Google's real published thresholds only
(e.g. LCP good <2.5s/needs work <4s/poor ≥4s) — never a guess. The findings-by-category chart
stacks each category's real findings by severity, from that audit's own counts — omit categories
with zero findings rather than padding the chart. Both are genuine data visualizations, not
decoration — never fabricate a number or trend to fill them in.

Then log the report in the audit's `CHANGELOG.md`.

## Step 4 — Prioritize

Rank each issue by:

| Severity | Meaning |
|---|---|
| 🔴 Critical | Blocking indexing/crawling, site broken for search engines |
| 🟠 High | Meaningfully hurting rankings or traffic |
| 🟡 Medium | Best-practice gap, moderate impact |
| 🟢 Low | Minor / cosmetic, nice-to-have |

Also note **effort**: Quick win (minutes), Moderate (hours), Major (dev project).

Fix order = highest severity + lowest effort first ("quick wins" first).

## Step 5 — Fix, using the step-by-step guides

For each issue, find (or create) its guide. Check `fixes/{category}/` for an existing one first
— reuse it as-is **only if it's genuinely site-agnostic** (no real domain, brand, page path, or
drafted copy anywhere in it). Otherwise create/use
`fixes/{category}/{site-domain}--{issue-name}.md`, scoped by site domain: a fix guide almost
always ends up with real specifics baked in (the actual CMS, real code snippets, real drafted
copy), so reusing one written for a *different* site under the same generic issue name hands the
client wrong instructions — wrong domain, wrong brand, wrong example — without anyone noticing.
When unsure whether a guide is generic enough to share, scope it: a duplicated generic guide
costs nothing, a misattributed specific one is a real error in delivered work.

Every fix guide follows the same beginner-friendly format:

1. **What's wrong** — plain-English explanation
2. **Why it matters** — impact on SEO
3. **How to check it yourself** — how to confirm the issue exists
4. **Step-by-step fix** — numbered, exact steps (with code snippets where relevant)
5. **How to verify the fix worked** — how to confirm it's resolved
6. **Tools to double-check** — free tools to re-test

If a guide doesn't exist yet for an issue, create one using `templates/fix-guide-template.md`.

If the issue is a **content problem** (thin content, duplicate/placeholder copy, a weak or
missing meta description, a poor/duplicate title tag, generic body copy), don't stop at telling
the client to "write real copy" — draft the actual replacement text for the real page(s)
affected, grounded in what's already on the live page (real product/location/service details,
the site's existing voice/terminology), using the guide's optional **7. Suggested rewritten
content** section. For a template shared across many pages, give 2-3 worked examples plus the
pattern to repeat, not one generic sample. Carry that drafted copy into the HTML report's fix
card too (a current-vs-suggested block), not just the steps.

## Step 6 — Verify

After fixes are applied, re-check each issue using the "How to verify" section of its guide.
Mark it resolved in `issue-tracker.md`.

## Step 7 — Log it

Update the audit folder's `CHANGELOG.md` (or the root one for repo-wide changes) with:
- Date
- What was fixed
- Who/what verified it

## Suggestions vs. fixes

Not everything is a "broken" issue — some findings are **opportunities** (e.g. "add FAQ schema
to increase rich result chances"). These get logged in `findings.md` too, but tagged
**💡 Suggestion** instead of a severity level, and are optional/lower priority by default.
