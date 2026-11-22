---
name: fortigate-vip-nat
description: >-
  Checklist for FortiGate virtual-IP / DNAT / port-forward craft via MCP.
  Resolve interfaces and VIP names; mutates need explicit verb. Skip when
  no VIP/NAT ask.
---

# FortiGate VIP / NAT

## Gate

User asked to list, create, update, or delete a FortiGate virtual IP,
DNAT, or port-forward. Prefer connected FortiGate MCP. Skip pure policy
ACL work without VIP (use `fortigate-policy-change`) and bare inventory.

Always load `fortigate-objects` and `fortigate-safety`.

## Checklist

1. **Authorize** — read/list is fine; create/update/delete need an
   explicit verb naming the VIP or create intent. **Done when** read
   proceeds or mutate verb is present (else refuse).
2. **Device / VDOM / interface** — resolve `device_id`; confirm VDOM;
   `list_interfaces` for `extintf`. **Done when** no invented interface.
3. **Existing VIP** — `list_virtual_ips` → `get_virtual_ip_detail` before
   update/delete. **Done when** name is from MCP or user paste.
4. **Addresses** — take `extip` / `mappedip` (and ports) from the user or
   inventory — never invent public/private mappings. **Done when** every
   address/port was supplied or listed.
5. **Blast radius** — state which published service remaps or stops.
   **Done when** risk was stated for mutates.
6. **Act** — `create_virtual_ip` / `update_virtual_ip` /
   `delete_virtual_ip`. **Done when** tool ran under authorization, or
   you stopped.
7. **Receipt** — device, vdom, VIP name, extip→mappedip (+ ports).
   **Done when** the reply has that shape; no secrets.

## Report shape

- Device id + VDOM
- VIP name
- External → mapped (+ portforward when set)
- Note if a matching firewall policy still needs a gated change
