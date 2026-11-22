---
name: velero-restore-run
description: >-
  Gated Velero restore checklist: prove Completed backup, scope namespaces and
  mapping, confirm, restore_create, restore_get. Prefer MCP.
---

# Velero restore run

## Gate

User authorized a **restore** from a Velero backup with an explicit verb.
Prefer `user-mcp_velero`. Skip when only inventory or status was asked.

Always load `velero-inventory`, `velero-mutate`, `velero-safety`, and skill
`velero`.

## Checklist

1. **Resolve backup** — `velero_backups_list` / `velero_backup_get` for the
   named backup. **Done when** backup exists and **phase=Completed** (or
   user accepts risk if not Completed).
2. **Scope** — `included_namespaces` and optional `namespace_mapping` from
   the ask; do not invent namespaces.
   **Done when** target namespaces are explicit in the plan.
3. **Risk statement** — warn overwrite impact on live objects; cite
   `velero-safety`.
   **Done when** user intent still matches restore after the warning.
4. **Confirm** — `velero_restore_create` with `backup_name`, restore `name`,
   **`confirm=true`**, and scoped namespaces/mapping.
   **Done when** MCP accepted the create.
5. **Prove** — `velero_restore_get` on the restore name; report phase.
   **Done when** receipt has restore name, phase, and namespaces.

## Report shape

- backup_name + backup phase (pre-restore)
- restore name + phase (post-create)
- namespaces / mapping summary
- overwrite warning acknowledged
- no credentials

