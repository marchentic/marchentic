# kopia

Agnostic Kopia craft: repository and snapshot inventory, repo status, and
gated snapshot/restore/forget via CLI. No Kopia MCP discovered — use
authenticated `kopia`; do not invent MCP tools. Treat restores as
overwrite-shaped; keep repository passwords out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `kopia-inventory` | Repo status, snapshot/policy list via CLI |
| `kopia-mutate` | Gated snapshot / restore / forget / maintenance |
| `kopia-safety` | Read-only default, explicit verbs, restore risk, credential refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `kopia` | Index / gate / procedure |
| `kopia-repo-status` | Repo status → recent snapshots → policy/maintenance |
| `kopia-restore-run` | Prove snapshot → DEST → warn → restore |

## Commands

- `/kopia` → Kopia inventory or gated craft
- `/kopia-status` → Repository health and recent coverage
- `/kopia-restore` → Gated restore checklist

## Related capabilities

- Other backup products and cluster-backup controllers are out of scope —
  this plugin owns Kopia repository/snapshot surfaces via CLI only.

## Diagrams

- [`docs/kopia-workflow.drawio`](docs/kopia-workflow.drawio) — gate → route →
  inventory / status / restore-mutate branches
