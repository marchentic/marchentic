---
name: proxmox-guest-ops
description: >-
  Checklist for gated Proxmox VM/LXC power, clone, and migrate: resolve
  guest, respect sacred deny-lists, explicit verb, follow task UPID.
  Prefer MCP. Skip when no guest-op ask.
---

# Proxmox guest ops

## Gate

User asked to start/stop/shutdown/reboot/pause/resume, clone, or migrate
a named (or clearly selected) VM/LXC. Prefer connected Proxmox MCP.
Skip pure inventory and skip disk/backup/cloud-init-only asks (those
still use `proxmox-safety` directly).

Always load `proxmox-inventory` and `proxmox-safety`.

## Checklist

1. **Resolve** — `proxmox_get_vms` / status with exact node+VMID or name
   match. **Done when** node + VMID + type (qemu/lxc) are known from
   MCP or paste.
2. **Sacred check** — if the consuming repo marks the VMID sacred /
   deny-listed, refuse power/clone/migrate/delete and say why.
   **Done when** sacred check passed or refused.
3. **Verb** — require an explicit power/clone/migrate verb this turn
   naming the guest. Prefer shutdown over stop unless force asked.
   **Done when** the verb + VMID are explicit.
4. **Act** — call the matching MCP tool (`proxmox_start_*`,
   `proxmox_shutdown_*`, `proxmox_stop_*`, `proxmox_reboot_*`,
   `proxmox_pause_vm` / `proxmox_resume_vm`, `proxmox_clone_*`,
   `proxmox_migrate_vm`). For clone, require `newid` (use
   `proxmox_get_next_vmid` when the user did not pick one and asked you
   to allocate). For migrate, require target node. **Done when** the
   tool returned (often a UPID).
5. **Follow task** — `proxmox_get_task_status` when a UPID exists; then
   re-read `proxmox_get_vm_status`. **Done when** status matches the
   intended end state or a clear failure is reported.
6. **Stop** — do not chain delete/resize/network changes unless also
   explicitly authorized. **Done when** reply has node+VMID+action+
   result.

## Report shape

- Node + VMID + type + name
- Action + UPID/result
- Post status
- One next check (wait, inventory, or stop)
