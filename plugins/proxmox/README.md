# proxmox

Agnostic Proxmox VE craft: list nodes/VMs, status, and gated
power/clone/migrate via MCP. Prefer Proxmox MCP; never invent VMID or
touch sacred hosts.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `proxmox-inventory` | MCP nodes/VMs/storage/pools/HA/RRD/status/config |
| `proxmox-safety` | Gated power, clone, migrate, delete, resize, backup |

## Skills

| Skill | Purpose |
| --- | --- |
| `proxmox` | Index / gate / procedure |
| `proxmox-guest-ops` | Power / clone / migrate checklist |

## Commands

- `/proxmox` → Inventory: nodes, VMs/LXC, storage, status
- `/proxmox-guest` → Gated power, clone, or migrate

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/proxmox-workflow.drawio`](docs/proxmox-workflow.drawio) — gate → route → inventory / guest-ops / refuse
