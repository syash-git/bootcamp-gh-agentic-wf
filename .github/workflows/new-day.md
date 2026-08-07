---
name: New Day
description: Add the current UTC date to the site's Daily Updates navigation and dialogs.
on:
  schedule: daily
  workflow_dispatch:
engine: copilot
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

Use the workflow run's current UTC date to update `index.html`.

First inspect every existing Daily Updates navigation control and daily update dialog. Determine the current UTC date at run time, then check for that date by its visible wording, navigation target, dialog ID, and accessible label/description IDs. If the UTC date is already represented, or adding it would duplicate a date, navigation control, or dialog, make no file changes and use `noop` with a brief explanation.

Otherwise, edit only `index.html`:

- Add one navigation list item for the UTC date under the existing Daily Updates navigation.
- Add exactly one matching accessible native dialog that confirms the daily update ran.
- Follow the existing HTML structure, month-day ID conventions, ordinal date wording, classes, attributes, and styling hooks exactly.
- Keep the navigation control's `aria-controls` synchronized with the dialog ID, and give the dialog matching `aria-labelledby` and `aria-describedby` references to unique elements inside it.
- Preserve every existing daily update and all unrelated HTML.
- Do not edit `styles.css` or any other file.

After making a change, use the `create-pull-request` safe output to create at most one pull request containing only `index.html`. Use a concise title and explain the UTC date added. If no change is needed, do not create a pull request.