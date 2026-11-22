# velero

Agnostic Velero craft: backup and restore inventory, fleet status, and gated
create/delete via MCP. Prefer `user-mcp_velero`; discover-first; treat restores
as overwrite-shaped; keep BSL credentials out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `velero-inventory` | List/get backups, restores, schedules, BSLs, uploads, summary |
| `velero-mutate` | Gated create/delete backup, restore, schedule via MCP |
| `velero-safety` | Read-only default, confirm gates, restore risk, credential refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `velero` | Index / gate / procedure |
| `velero-status-check` | status_summary → failures → schedule last-backup sweep |
| `velero-restore-run` | Completed backup → scope → confirm → restore create/get |

## Commands

- `/velero` → Velero inventory or gated craft
- `/velero-status` → Fleet health and failed backup pass
- `/velero-restore` → Gated restore checklist

## Related capabilities

- Cluster API triage and GitOps sync are out of scope — this plugin owns
  Velero CR surfaces via MCP only.

## Diagrams

- [`docs/velero-workflow.drawio`](docs/velero-workflow.drawio) — gate → route →
  inventory / status / restore-mutate branches
