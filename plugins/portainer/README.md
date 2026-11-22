# portainer

Agnostic Portainer craft: endpoint/stack/container inventory and gated
stack/container mutations via API/UI. No Portainer MCP in the live
harness catalog — resolve a base URL; never invent endpoint ids; keep
tokens out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `portainer-endpoints` | Endpoint/environment list, resolve, health |
| `portainer-stacks` | Stack inventory and gated deploy/update/delete |
| `portainer-containers` | Container inventory and gated stop/remove/logs |
| `portainer-safety` | Deploy/stop/delete/prune gates; credential refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `portainer` | Index / gate / procedure |
| `portainer-endpoint-audit` | Endpoint fleet inventory checklist |
| `portainer-stack-deploy` | Gated stack deploy/update checklist |

## Commands

- `/portainer` → Portainer endpoint/stack/container craft
- `/portainer-audit` → Endpoint fleet audit
- `/portainer-stack` → Gated stack deploy/update

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/portainer-workflow.drawio`](docs/portainer-workflow.drawio) — gate → route → inventory / stack deploy / gated mutate
