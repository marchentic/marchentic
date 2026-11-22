# argocd

Agnostic Argo CD craft: list/get apps, sync status, and gated sync/action
via MCP. Prefer Argo CD MCP; never invent app names.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `argocd-apps` | MCP list/get/tree/events/resources/logs/projects/clusters |
| `argocd-sync` | Gated sync, prune, resource actions, Application CRUD |

## Skills

| Skill | Purpose |
| --- | --- |
| `argocd` | Index / gate / procedure |
| `argocd-app-status` | Application health/sync triage checklist |

## Commands

- `/argocd` → Application status, tree, or events
- `/argocd-sync` → Gated sync, prune, or resource action

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/argocd-workflow.drawio`](docs/argocd-workflow.drawio) — gate → route → status / sync / action
