---
name: Weekly Report Status
description: Publish a concise weekly repository activity report.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
strict: true
engine: copilot
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

## Task

Publish exactly one new issue containing a concise activity report for the
previous seven days, ending when this workflow starts. Review repository commits,
issues, and pull requests created or updated in that period.

Use GitHub data through the configured GitHub tool. Do not create, edit, or close
any resources except the single report issue through `create-issue`.

The issue title must identify the seven-day reporting window. Write the report in
GitHub-flavored Markdown with these sections:

- `### Summary` — a short overview with activity counts.
- `### Commits` — notable commits or a clear statement that no commits occurred.
- `### Issues` — notable created or updated issues or a clear statement that no
  issue activity occurred.
- `### Pull Requests` — notable created, updated, merged, or closed pull
  requests or a clear statement that no pull request activity occurred.

State clearly in the summary and each applicable section when no activity
occurred during the reporting window. Always publish the report issue, including
when there was no activity in any category.
