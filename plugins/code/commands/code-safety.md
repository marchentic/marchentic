---
name: code-safety
description: >-
  Agent/workspace blast-radius audit: remote DBs in tests, unbounded deletes,
  infra destroy flags, prose-only rules, MCP/harness bypass, CI agents with
  secrets. Read-only; names and paths only. Apply fixes only after approval.
---

# /code-safety

Load and follow `code-safety` now on the scope the user named (folder,
package, whole repo + discoverable harness config). Default: whole repo.

Audit first. Change no code unless the user explicitly asks to apply named
in-repo fixes after the report. Never print secret values.
