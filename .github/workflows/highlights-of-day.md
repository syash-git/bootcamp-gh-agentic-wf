---
name: Highlights of Day
description: Add an unused GitHub Agentic Workflows FAQ to today's Daily Update.
on:
  schedule: every 6 hours
  workflow_dispatch:
engine: copilot
permissions:
  contents: read
  copilot-requests: write
network:
  allowed:
    - github.github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# Highlights of Day

Use the workflow run's current UTC date to update `index.html` with one FAQ from the GitHub Agentic Workflows FAQ.

Fetch <https://github.github.com/gh-aw/reference/faq/> with the `web-fetch` tool. Inspect every existing Daily Updates navigation control and dialog in `index.html`, and compare their questions and answers with the fetched FAQ content. Select one FAQ question that is not already represented anywhere in `index.html`; preserve its meaning and write a concise, accurate answer based only on the fetched FAQ.

Before editing, locate the dialog for the current UTC date by its visible ordinal date wording, navigation target, dialog ID, and accessible label/description IDs:

- If today's dialog already contains an FAQ, make no changes and use `noop` with a brief explanation.
- If no unused FAQ remains, make no changes and use `noop` with a brief explanation.
- If today's date has a placeholder dialog, reuse its existing navigation control and dialog. Replace only the placeholder question and answer with the selected FAQ.
- Otherwise, add exactly one matching Daily Updates navigation control and one accessible native dialog for today's UTC date.

Edit only `index.html`. Follow the existing HTML structure, month-day ID conventions, ordinal date wording, classes, attributes, and styling hooks exactly. Keep the navigation control's `aria-controls` synchronized with the dialog ID, and give the dialog matching `aria-labelledby` and `aria-describedby` references to unique question and answer elements. Preserve every existing update and all unrelated HTML. Never duplicate a date, navigation control, dialog, or FAQ. Do not edit `styles.css` or any other file.

After making a change, use the `create-pull-request` safe output to create at most one pull request containing only `index.html`. Use a concise title and identify the UTC date and FAQ added. If no change is needed, do not create a pull request.