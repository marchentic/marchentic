# harbor

Agnostic Harbor registry craft: projects/repos/artifacts inventory and
gated delete/retention/robot changes via API/UI. No Harbor MCP in the
live harness catalog — resolve a base URL; never invent project or digest
names; keep robot tokens out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `harbor-projects` | Project list, resolve, visibility |
| `harbor-artifacts` | Repo/artifact/tag/scan inventory |
| `harbor-safety` | Delete/retention/robot/ACL gates; credential refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `harbor` | Index / gate / procedure |
| `harbor-project-audit` | Project fleet inventory checklist |
| `harbor-retention-run` | Gated retention purge checklist |

## Commands

- `/harbor` → Harbor project/artifact craft
- `/harbor-audit` → Project fleet audit
- `/harbor-retention` → Gated retention purge

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/harbor-workflow.drawio`](docs/harbor-workflow.drawio) — gate → route → inventory / retention / gated mutate
