# freshservice

Agnostic Freshservice ITSM craft — create gates (create-only by default), ticket
body shape, additive updates, and honest status. Install when the project uses
Freshservice (MCP or configured API). No Freshservice MCP is assumed; do not
invent tool names.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `freshservice-create` | Create-only filing gate, types, never invent ids |
| `freshservice-ticket` | Overview / Impact / Details / outcome body shape |
| `freshservice-update` | Edit existing tickets; prefer notes over rewrites |
| `freshservice-status` | Status / priority / assign honesty |

All rules are **agent-requested** (`alwaysApply: false`).

## Skills

| Skill | Purpose |
| --- | --- |
| `freshservice` | Gate / load map / defaults / procedure |
| `freshservice-ticket-author` | Body authoring + create/update checklist |

## Commands

- `/freshservice` → ticket create, update, and status craft

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/freshservice-workflow.drawio`](docs/freshservice-workflow.drawio) — gate → route → create/update/status → evidence
