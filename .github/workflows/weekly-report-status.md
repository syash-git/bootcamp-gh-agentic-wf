---
name: Weekly Report Status
description: Publish a concise weekly report of repository activity.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
engine: copilot
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
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

Generate a concise activity report for this repository covering the previous seven full days, from seven days before the workflow start time up to the workflow start time, in UTC.

Use GitHub data to summarize:

- commits pushed during the reporting window
- issues opened, closed, or otherwise updated during the reporting window
- pull requests opened, merged, closed, or otherwise updated during the reporting window

Include the UTC reporting window and compact totals for each category. Use `###` headings for report sections and link to relevant GitHub items when useful. Do not invent activity or metadata.

Always publish exactly one new issue using the `create-issue` safe output. If there was no activity in any category, state clearly in the issue body that no commits, issue activity, or pull request activity occurred during the reporting window.