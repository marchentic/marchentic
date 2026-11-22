---
name: velero-status
description: >-
  Velero fleet health: status summary, failed backups, schedule last-run check.
---

# /velero-status

1. If the user did not authorize a Velero health/status check, stop.
2. Load skill `velero` and `velero-status-check` with rules `velero-inventory`
   and `velero-safety`.
3. Prefer `user-mcp_velero`: `velero_status_summary` → failed backups →
   schedule last backup sweep.
4. Return summary + failures + schedule notes and one next step.
