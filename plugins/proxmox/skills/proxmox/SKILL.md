---
name: proxmox
description: >-
  Agnostic Proxmox VE craft: list nodes/VMs, status, and gated
  power/clone/migrate via MCP. Prefer Proxmox MCP; never invent VMID or
  touch sacred hosts. Skip when the user did not authorize this surface.
---

# Proxmox

## Gate

No explicit Proxmox / VM / LXC / node ask and no named VMID → **skip**.
Prefer a connected MCP. Bare product name alone is not enough for a
broad mutate.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list nodes/VMs, status, config, storage, pools, HA, RRD |
| Power | start, stop, shutdown, reboot, pause, resume |
| Clone / create / migrate | clone, create, migrate, template |
| Disk / net / cloud-init | resize, add disk, network, cloud-init |
| Snapshot / backup | snapshot, backup, restore, forget |
| Guest command | execute command inside VM |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / status / config / storage / pools / RRD / tasks | `proxmox-inventory` |
| Power / clone / migrate / delete / resize / backup gates | `proxmox-safety` |
| Guest ops checklist (power/clone/migrate) | `proxmox-safety` · skill `proxmox-guest-ops` |

## Defaults

1. Never invent node name, VMID, storage id, or `newid` — list/resolve.
2. Read-only inventory is the default.
3. Respect host sacred VMs / deny-lists when the consuming repo defines
   them.
4. Prefer MCP tools discovered on the live Proxmox MCP; do not invent
   tool names.
5. Prefer graceful shutdown over hard stop unless force was asked.
6. After mutates, follow UPIDs with `proxmox_get_task_status` before
   claiming success.
7. Guest OS packaging and app deploys inside the VM are out of scope.

## Procedure

1. Decide the surface (inventory vs power vs clone/migrate vs
   disk/net vs snapshot/backup vs guest command). **Done when** you can
   name one surface, or you skipped because none was asked.
2. Resolve ids from MCP (`proxmox_get_nodes`, `proxmox_get_vms`, status)
   or from ids the user pasted. **Done when** every id you will use was
   listed/read, or you stopped instead of inventing one.
3. Follow the load-map rule (and `proxmox-guest-ops` for power/clone/
   migrate). Apply `proxmox-safety` before any mutate. **Done when**
   inventory evidence matches the ask, or the authorized mutate
   completed and task/status was re-read.
4. Stop after evidence unless the user also used an explicit mutate
   verb. **Done when** the reply has node+VMID + status (or task
   result), and no unauthorized destructive op ran.
