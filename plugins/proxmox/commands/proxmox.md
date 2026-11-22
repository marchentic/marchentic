---
name: proxmox
description: >-
  Proxmox VE inventory: nodes, VMs/LXC, storage, status via MCP.
---

# /proxmox

1. If the user did not authorize Proxmox / VM / LXC work, say so and
   stop.
2. Load `proxmox` with rule `proxmox-inventory`.
3. Prefer Proxmox MCP. List/resolve nodes and VMIDs before inventing
   them; never invent storage ids.
4. Return node + VMID/status (or inventory table). For explicit
   power/clone/migrate, prefer `/proxmox-guest` and `proxmox-safety`.
