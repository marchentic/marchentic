---
name: velero-status-check
description: >-
  Velero health checklist: status_summary, failed backups, schedule last-backup
  sweep. Prefer MCP. Skip when no status/health ask.
---

# Velero status check

## Gate

User asked whether Velero is healthy, what failed, whether backups are
running, or for a short fleet status pass. Prefer `user-mcp_velero`. Skip
pure single-backup get (use `velero-inventory`) and mutate paths.

Always load `velero-inventory`, `velero-safety`, and skill `velero`.

## Checklist

1. **Summary** — `velero_status_summary`.
   **Done when** headline counts or top-level failures are captured.
2. **Failed backups** — `velero_backups_list` with `phase` narrowed to
   failed (or filter from summary), then `velero_backup_get` on top names.
   **Done when** each cited failure has name + phase + namespaces.
3. **Schedules** — `velero_schedules_list`; for schedules in scope,
   `velero_schedule_get` and note last backup / paused state when present.
   **Done when** each focused schedule has last-run evidence or explicit "no
   last backup yet."
4. **Optional uploads** — when CSI/move data issues are suspected,
   `velero_datauploads_list` scoped by `backup_name` from step 2.
   **Done when** upload errors tie to a named backup or step is skipped.
5. **Safety** — inventory only unless user also authorized mutate.
   **Done when** receipt has no unauthorized delete/restore.

## Report shape

- Summary highlight from `velero_status_summary`
- Failed backups table: name, phase, namespaces
- Schedule lines: name, cron hint, last backup / pause note
- One recommended next step (fix backup, restore drill, or gated mutate)

