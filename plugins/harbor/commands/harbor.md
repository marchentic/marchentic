---
name: harbor
description: >-
  Harbor project/artifact craft via API/UI.
---

# /harbor

1. If the user did not authorize Harbor work, say so and stop.
2. Load `harbor` with rules `harbor-projects` / `harbor-artifacts` /
   `harbor-safety` as the load map requires.
3. Prefer Harbor API/UI (no Harbor MCP in the live catalog). Never invent
   project, repo, or digest names.
4. Return project + repo/tag + short finding (no tokens). For fleet
   audits prefer skill `harbor-project-audit` or `/harbor-audit`; for
   retention purge prefer `harbor-retention-run` or `/harbor-retention`.
