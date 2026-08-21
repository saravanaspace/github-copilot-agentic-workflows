---
name: New Day
description: Add the current UTC date as a daily update in the site navigation.
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine: copilot
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

## Task

Use the workflow run's UTC date. Determine it at runtime with `date -u +%F`;
do not use the runner's local date or infer the date from the repository.

Inspect `index.html` before editing. Preserve all existing daily updates and do
not modify `styles.css` or any other file.

Follow the existing Daily Updates HTML structure exactly:

1. Add one navigation control to the existing `daily-updates-list` using the
   existing button classes and accessibility attributes.
2. Add one matching accessible `dialog` using the existing
   `daily-update-dialog` structure, including `aria-labelledby`,
   `aria-describedby`, the existing close control, and matching question and
   answer IDs.
3. Use the page's existing ordinal date wording, such as `1st of August`, and
   its lowercase `month-day` ID convention, such as `august-1-dialog`.
4. Make the dialog text clearly confirm that the daily update ran on that UTC
   date.

Before making any edit, check for the UTC date's existing navigation control,
dialog, and IDs. If any already represent that date, make no change and call
`noop` with a short explanation. Do not duplicate a date, navigation control,
or dialog.

If a change is needed, update only `index.html` and create at most one pull
request through the configured `create-pull-request` safe output. Do not use
any other write mechanism.
