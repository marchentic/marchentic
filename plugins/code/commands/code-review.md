---
name: code-review
description: >-
  Quality review of a change: correct, safe, holds under load, tested, fast,
  lean. Reads connected code, not only the diff. Numbered findings with
  concrete cases.
---

# /code-review

1. Collect the review target (uncommitted, staged, branch, PR, or named files).
   Default: uncommitted changes, or the last commit if the tree is clean.
2. Collect changed paths and a diff/status summary for the Task prompt (do not
   expect the reviewer to run git).
3. Launch `code-reviewer` (read-only) with that evidence.
4. Relay the report unchanged in structure: What this change does →
   Must/Should/Nice findings → Verdict / Lean / Not checked → next parent
   action.
5. Change no code in this command turn unless the user explicitly asked to
   apply fixes after the report.
