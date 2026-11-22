---
name: zot
description: >-
  Zot repository/tag craft via API/UI.
---

# /zot

1. If the user did not authorize Zot work, say so and stop.
2. Load `zot` with rules `zot-repos` / `zot-tags` / `zot-safety` as the
   load map requires.
3. Prefer Zot API/UI (no Zot MCP in the live catalog). Never invent repo
   or tag names.
4. Return repo + tag + short finding (no credentials). For fleet audits
   prefer skill `zot-repo-audit` or `/zot-audit`; for GC prefer
   `zot-gc-run` or `/zot-gc`.
