---
name: velero
description: >-
  Velero inventory, status, or gated backup/restore/schedule craft via MCP.
---

# /velero

1. If the user did not authorize Velero backup/restore work, say so and stop.
2. Load skill `velero` with rules `velero-inventory`, `velero-mutate`, and
   always `velero-safety`.
3. Prefer `user-mcp_velero`. List before get; never invent backup, schedule,
   or restore names.
4. Return name + phase + namespaces (read) or action + confirm receipt
   (mutate). For status passes use skill `velero-status-check`; for restores
   use skill `velero-restore-run` or `/velero-restore`.
