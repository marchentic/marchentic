---
name: obsidian-audit
description: >-
  Obsidian vault inventory and health: list notes, orphans, broken wikilinks.
---

# /obsidian-audit

1. If the user did not authorize a vault inventory / health check, say so
   and stop.
2. Load `obsidian` and skill `obsidian-vault-audit` with rules
   `obsidian-vault` / `obsidian-safety`.
3. Prefer MCP when ready; else filesystem under a resolved root. Never
   invent paths; do not auto-delete orphans.
4. Return scope + counts + capped path list (no vault dumps) and one next
   step.
