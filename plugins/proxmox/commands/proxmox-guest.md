---
name: proxmox-guest
description: >-
  Gated Proxmox VM/LXC power, clone, or migrate on a named guest.
---

# /proxmox-guest

1. If the user did not authorize a power / clone / migrate (or other
   guest mutate), say so and stop.
2. Load `proxmox` and skill `proxmox-guest-ops` with rules
   `proxmox-inventory` / `proxmox-safety`.
3. Prefer Proxmox MCP. Require an explicit verb naming node+VMID.
   Respect sacred deny-lists; prefer shutdown over hard stop.
4. Return node + VMID + action + task/status. No unauthorized mass ops.
