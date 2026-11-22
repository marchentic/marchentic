# fortigate

Agnostic FortiGate craft: inventory policies/addresses/routes and gated
firewall changes via MCP. Prefer FortiGate MCP; never invent policy ids;
destructive needs explicit verb.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `fortigate-inventory` | Devices, health, VDOMs, interfaces via MCP |
| `fortigate-policies` | Firewall policy list/detail/create/update/delete |
| `fortigate-objects` | Address, service, and virtual-IP (NAT) craft |
| `fortigate-routes` | Routing table + static route craft |
| `fortigate-safety` | Destructive gates; read-only default; no secret echo |

## Skills

| Skill | Purpose |
| --- | --- |
| `fortigate` | Index / gate / procedure |
| `fortigate-policy-change` | Gated policy create/update/delete checklist |
| `fortigate-vip-nat` | Virtual-IP / DNAT / port-forward checklist |

## Commands

- `/fortigate` → FortiGate inventory or gated change
- `/fortigate-policy` → Gated firewall policy mutate

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/fortigate-workflow.drawio`](docs/fortigate-workflow.drawio) — gate → route → inventory / policy / VIP / routes
