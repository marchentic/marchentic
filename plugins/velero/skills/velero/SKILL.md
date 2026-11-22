---
name: velero
description: >-
  Agnostic Velero craft: backup/restore inventory, status, and gated
  create/delete via MCP. Prefer user-mcp_velero; discover-first; restores are
  overwrite-shaped. Skip when the user did not authorize this surface.
---

# Velero

## Gate

No explicit Velero / backup-restore via Velero ask (and no named backup,
schedule, or restore on the Velero MCP) → **skip**. Bare "back up the
cluster" without Velero is out of scope. Prefer a connected Velero MCP.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list backups, restores, schedules, BSLs, data uploads |
| Status | health, failed backups, last schedule run, fleet summary |
| Backup create | on-demand backup, TTL, namespaces, snapshot data |
| Restore | restore from backup, namespace mapping |
| Schedule | cron backup schedule create/delete |
| Delete | delete backup, restore, or schedule |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / get backups, restores, schedules, BSL, uploads | `velero-inventory` |
| Create / delete backup, restore, schedule | `velero-mutate` |
| Health / failed backup sweep | skill `velero-status-check` |
| Restore run checklist | skill `velero-restore-run` |
| Gates, confirm, restore risk, refuse | `velero-safety` (always) |

## Defaults

1. Never invent backup, schedule, or restore names — list/resolve first.
2. Prefer `user-mcp_velero`; use only tools on the live MCP map.
3. Read inventory before any mutate (`velero-inventory`).
4. `confirm=true` on destructive MCP tools per `velero-safety`.
5. BSL list is read-only; GitOps owns BSL YAML.
6. Cluster API triage and GitOps sync are out of scope — this plugin owns
   Velero CR craft via MCP.
7. Non-Velero backup products are out of scope.

## Procedure

1. Decide the surface (inventory / status / backup / restore / schedule /
   delete). **Done when** you can name one surface, or you skipped because
   none was asked.
2. Resolve names from MCP lists or user paste; never invent.
   **Done when** every name used in gets or mutates was listed/read this turn.
3. Follow the load-map rule and compound skill when status or restore run
   is in play. Always apply `velero-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: name + phase + namespaces (inventory), or
   action + confirm + post-get phase (mutate). **Done when** evidence is
   cited and overwrite risk was stated for restores.
