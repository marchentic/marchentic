# zot

Agnostic Zot OCI registry craft: repository/tag inventory and gated
delete/GC via API/UI. No Zot MCP in the live harness catalog — resolve a
base URL; never invent repo or tag names; keep credentials out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `zot-repos` | Repository list and resolve |
| `zot-tags` | Tag/manifest/referrer inventory |
| `zot-safety` | Delete/GC/auth gates; credential refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `zot` | Index / gate / procedure |
| `zot-repo-audit` | Repository fleet inventory checklist |
| `zot-gc-run` | Gated garbage-collection checklist |

## Commands

- `/zot` → Zot repository/tag craft
- `/zot-audit` → Repository fleet audit
- `/zot-gc` → Gated garbage collection

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/zot-workflow.drawio`](docs/zot-workflow.drawio) — gate → route → inventory / GC / gated mutate
