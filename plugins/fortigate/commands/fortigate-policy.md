---
name: fortigate-policy
description: >-
  Gated FortiGate firewall policy create/update/delete via MCP.
---

# /fortigate-policy

1. If the user did not authorize a FortiGate policy change, say so and
   stop.
2. Load `fortigate` and skill `fortigate-policy-change` with rules
   `fortigate-policies` / `fortigate-safety` (and objects/inventory as
   needed to resolve names).
3. Prefer FortiGate MCP. Resolve device_id and policy_id first; refuse
   mutate without an explicit verb.
4. Return device + vdom + policy id/name + change summary (no secrets).
