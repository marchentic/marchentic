---
name: obsidian
description: >-
  Obsidian vault inventory or gated note act.
---

# /obsidian

1. If the user did not authorize Obsidian / vault work, say so and stop.
2. Load `obsidian` with rules `obsidian-vault` / `obsidian-safety`.
3. Prefer MCP when ready; else the vault filesystem. Never invent vault
   roots or note paths.
4. Return relative path(s) + what changed or was found (no vault dumps).
   For authoring prefer skill `obsidian-note-author`; for inventory/health
   prefer `obsidian-vault-audit` or `/obsidian-audit`.
