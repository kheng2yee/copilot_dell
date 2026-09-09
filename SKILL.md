---
name: make-calendar
description: Build a formatted monthly calendar grid (weekday headers, correctly placed dates, shaded weekends, highlighted today) on a new sheet. Use when the user asks to "insert a calendar", "make a calendar for <month>", "add a planner grid", or names a month/year to lay out. Reads the target month and year from the request; defaults to the current month.
---

# Calendar

Draw a clean monthly calendar onto a new sheet (unless otherwise specified): a title row, a weekday
header, and a 6-week date grid with weekends shaded and today highlighted.

## When to use

- The user asks for a calendar, planner grid, or month layout, optionally naming
  a month and/or year.

## When NOT to use

- The user wants a plain list of dates in a column.

## Inputs

- **Month**: from the request (a name like "September" or a number). If none,
  use the current month.
- **Year**: from the request. If none, use the current year.

## Layout (on a new sheet)

1. **Title row** spanning 7 columns: the month name and year (e.g.
   "September 2026"), centered, bold, white text on a dark blue fill.
2. **Weekday header row**: Sun, Mon, Tue, Wed, Thu, Fri, Sat, centered, bold,
   white text on a medium blue fill.
3. **Date grid**: 6 rows by 7 columns. Place day numbers on the correct
   weekdays. Compute the weekday of the 1st of the month and the number of days
   in the month; leave cells before the 1st and after the last day blank. Dates
   sit top-right in tall (about 34pt) cells so the grid reads like a planner.

## Formatting rules

- Shade the Sunday and Saturday columns of the date grid a light gray.
- If the month being drawn is the actual current month, highlight today's date
  cell with a soft yellow fill and bold it. Otherwise highlight nothing.
- Put thin light-gray borders around all cells of the whole block and set the 7
  columns to a roughly equal, generous width (~90px).

## Important rules (avoid the merge error)

- Before writing anything, **clear and unmerge the entire target block first**,
  then build it. A re-run over an existing calendar must not fail.
- Prefer **Center Across Selection** for the title instead of a real merge if
  merging is unreliable in this host; both look the same. If you do merge, merge
  the empty cells first and only then write the title text into the merged cell.
- Never write a multi-column value array into an unmerged single row expecting it
  to span; either merge/center-across first, or write the title into one cell.
