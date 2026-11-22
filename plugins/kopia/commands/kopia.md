---
name: kopia
description: >-
  Kopia inventory, status, or gated snapshot/restore/forget craft via CLI.
---

# /kopia

1. If the user did not authorize Kopia repository/snapshot work, say so and stop.
2. Load skill `kopia` with rules `kopia-inventory`, `kopia-mutate`, and
   always `kopia-safety`.
3. Prefer authenticated `kopia` CLI (no Kopia MCP discovered — do not invent
   tools). List before mutate; never invent snapshot ids or repo paths.
4. Return snapshot id + source + time (read) or action + path/DEST receipt
   (mutate). For status passes use skill `kopia-repo-status`; for restores
   use skill `kopia-restore-run` or `/kopia-restore`.
