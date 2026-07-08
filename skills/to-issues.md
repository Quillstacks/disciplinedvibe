---
name: to-issues
description: Slice a PRD into independently grabbable vertical-slice issues.
---

# to-issues

Break the PRD in `issues/PRD.md` into independently grabbable issues, written as
local markdown files in `issues/` (one file per issue, e.g. `issues/01-*.md`).

Rules:

1. Slice vertically, not horizontally. A good slice cuts through every layer
   (data, service, dashboard) and produces something visible and testable. A bad
   slice is "all the schema" or "all the dashboard".
2. The first slice must be a tracer bullet: the thinnest end-to-end path that
   proves the whole flow works.
3. Record blocking relationships between issues (which must be done before which),
   so independent issues could be worked in parallel.
4. Each issue states: title, the user-facing outcome, and how it will be tested.

If your first proposed slice is horizontal, reject it and re-slice before writing
the files.
