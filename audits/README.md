# Audits

Each site audit gets its own folder here, named `{site-name}-{YYYY-MM-DD}/`, containing:

- `findings.md` — raw findings (from `templates/audit-report-template.md`)
- `issue-tracker.md` — prioritized issue list (from `templates/issue-tracker-template.md`)
- `CHANGELOG.md` — log of fixes applied and verified for that audit

Example:
```
audits/
└── example-com-2026-09-04/
    ├── findings.md
    ├── issue-tracker.md
    └── CHANGELOG.md
```

No audits have been run yet — this folder will fill up as we work through real sites.
