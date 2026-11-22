---
name: fortigate
description: >-
  Agnostic FortiGate craft: inventory policies/addresses/routes and gated
  firewall changes via MCP. Prefer FortiGate MCP; never invent policy ids;
  destructive needs explicit verb. Skip when the user did not authorize
  this surface.
---

# FortiGate

## Gate

No explicit FortiGate / FortiGate firewall / FortiGate policy / VIP /
static-route ask and no named device_id or policy → **skip**. Bare
"firewall" without FortiGate is out of scope. Prefer a connected
FortiGate MCP (`user-mcp_fortigate`). Bare product name alone is not
enough for mutates.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | devices, health, status, VDOM, interfaces |
| Policies | list/inspect/create/update/delete firewall policy |
| Objects / VIP | address, service, virtual IP / DNAT / port-forward |
| Routes | routing table, static route create/update/delete |
| Mutate | any create/update/delete or add/remove device |

## Load map

| Need | Rule / skill |
| --- | --- |
| Devices / health / interfaces / VDOMs | `fortigate-inventory` |
| Firewall policy craft | `fortigate-policies` · skill `fortigate-policy-change` |
| Address / service / VIP | `fortigate-objects` · skill `fortigate-vip-nat` |
| Static routes / FIB | `fortigate-routes` |
| Destructive policy / object / route / device | `fortigate-safety` |

## Defaults

1. Never invent `device_id`, `policy_id`, object/VIP names, `route_id`,
   or VDOM — list/resolve first.
2. Read-only is the default for network devices.
3. Irreversible ACL/NAT/route changes: state risk; require clear
   authorization (`fortigate-safety`).
4. Prefer MCP tools discovered on the live FortiGate MCP; do not invent
   tool names.
5. Prefer the smallest mutate; reuse listed objects before creating new
   ones.
6. Operator replies: device + vdom + id/name + short finding — no
   passwords or API tokens.
7. Neighbor firewall products and site overlays are out of scope except
   as ids resolved from this MCP.

## Procedure

1. Decide the surface (inventory vs policies vs objects/VIP vs routes vs
   mutate). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Resolve ids from MCP (`list_devices`, list/detail tools) or from ids
   the user pasted. **Done when** every id you will use was listed/read,
   or you stopped instead of inventing one.
3. Follow the load-map rule (and compound skill for policy change or
   VIP/NAT). Always apply `fortigate-safety` when a mutate is in play.
   **Done when** evidence matches the ask or the mutate was refused for
   lack of verb.
4. Stop after evidence unless the user also used an implement/mutate
   verb. **Done when** the reply has device (+ vdom) + id/name + finding
   or what changed, and no unauthorized mutate ran.
