---
name: fortigate-policy-change
description: >-
  Checklist for gated FortiGate firewall policy create/update/delete via
  MCP. Resolve device and policy ids; require explicit verb. Skip when no
  policy mutate ask.
---

# FortiGate policy change

## Gate

User asked to create, update, tighten, open, or delete a FortiGate
firewall policy (or named a policy id for a change). Prefer connected
FortiGate MCP. Skip pure inventory/status (use `fortigate-inventory`) and
VIP-only work (use `fortigate-vip-nat`).

Always load `fortigate-policies` and `fortigate-safety`.

## Checklist

1. **Authorize** — confirm an explicit mutate verb this turn naming the
   policy or create intent. **Done when** verb is present, or you refuse
   and stop.
2. **Device / VDOM** — `list_devices` → `device_id`; `discover_vdoms`
   when multi-VDOM or non-root named. **Done when** device (+ vdom) is
   resolved.
3. **Inventory objects** — `list_address_objects` / `list_service_objects`
   (and interfaces via `list_interfaces`) for every name you will put in
   `policy_data`. **Done when** no invented object/interface names remain.
4. **Existing policy** — for update/delete: `list_firewall_policies` →
   `get_firewall_policy_detail`. **Done when** `policy_id` is from MCP or
   user paste.
5. **Blast radius** — one sentence: traffic that will newly match or stop
   matching (esp. management paths / any-any). **Done when** risk was
   stated; refuse any-any without named src/dst/service/intf.
6. **Act** — `create_firewall_policy` / `update_firewall_policy` /
   `delete_firewall_policy` with resolved ids only. **Done when** the
   tool ran under authorization, or you stopped.
7. **Receipt** — device, vdom, policy id/name, change summary — no
   secrets. **Done when** the reply has that shape.

## Report shape

- Device id + VDOM
- Policy id/name
- Action (created / updated fields / deleted)
- One follow-up check (hit count / related VIP / route) when useful
