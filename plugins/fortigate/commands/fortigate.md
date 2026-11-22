---
name: fortigate
description: >-
  FortiGate inventory, policies, objects, or routes via MCP (gated mutates).
---

# /fortigate

1. If the user did not authorize FortiGate / FortiGate firewall work, say
   so and stop.
2. Load `fortigate` with the load-map rules for the surface (inventory /
   policies / objects / routes) and always `fortigate-safety` when a
   mutate is possible.
3. Prefer FortiGate MCP (`user-mcp_fortigate`). List/resolve device and
   object ids — never invent them.
4. Return device (+ vdom) + id/name + short finding. For policy mutates,
   prefer skill `fortigate-policy-change` or `/fortigate-policy`.
