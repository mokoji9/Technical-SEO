# Technical SEO Workflow

This is the process to follow every time we audit a website and fix issues.
Written for beginners — no assumed SEO background.

## Step 0 — Ask: Automated or Manual?

Every time an audit starts, always ask:

> "Do you want me to pull data automatically using connected SEO tools, or will you provide the data yourself (crawl export, Search Console, PageSpeed report, etc.)?"

- If **automated**: use available tools (Semrush, DataForSEO, site audit/crawl skills) to gather crawl data, performance data, backlinks, indexation status.
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

## Optional — Designed HTML report

If the audit is going to a client or stakeholder (not just internal reference), turn it into a
polished HTML report instead of handing over raw markdown. Start from
`templates/report-template.html` — it has the full design system (light/dark theming, severity
color-coding, stat tiles, finding cards) already built. Read the comment block at the top of
that file first: it explains what must be rebuilt per audit (the site's real accent color and
logo, all copy and findings) versus what's safe to reuse as-is (the CSS structure). Load the
`artifact-design` skill before starting, and publish it as a Claude Artifact.

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

For each issue, find (or create) its guide in `fixes/{category}/{issue-name}.md`.
Every fix guide follows the same beginner-friendly format:

1. **What's wrong** — plain-English explanation
2. **Why it matters** — impact on SEO
3. **How to check it yourself** — how to confirm the issue exists
4. **Step-by-step fix** — numbered, exact steps (with code snippets where relevant)
5. **How to verify the fix worked** — how to confirm it's resolved
6. **Tools to double-check** — free tools to re-test

If a guide doesn't exist yet for an issue, create one using `templates/fix-guide-template.md`.

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
