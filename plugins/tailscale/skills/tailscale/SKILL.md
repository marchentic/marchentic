---
name: tailscale
description: >-
  Agnostic Tailscale craft: devices, ACLs, and network inventory with gated
  ACL/device/key changes. Prefer tailscale CLI or Admin API (no Tailscale
  MCP discovered). Skip when the user did not authorize this surface.
---

# Tailscale

## Gate

No explicit Tailscale / tailnet / ACL / device / auth-key ask and no named
device or tag → **skip**. WireGuard-only or Headscale asks are out of
scope here. Prefer a connected Tailscale MCP when one exists; otherwise
`tailscale` CLI and/or Admin API with a resolved tailnet. Bare product
name alone is not enough for mutates.

Route by surface:

| Surface | Signals |
| --- | --- |
| Devices | status, online, tags, IPs, netmap, ping |
| ACLs | policy, grants, tagOwners, SSH ACL, tests |
| Keys / risk | auth key create/revoke, device delete, route advertise |

## Load map

| Need | Rule / skill |
| --- | --- |
| Devices / status / routes inventory | `tailscale-devices` |
| ACL / grants / tag policy | `tailscale-acls` |
| Minimal ACL change checklist | skill `tailscale-acl-change` |
| Delete / key / ACL widen / route ads | `tailscale-safety` |

## Defaults

1. Never invent device id, node name, ACL tag, or route prefix —
   list/resolve first.
2. Read-only inventory is the default. Mutate only with an explicit verb
   naming the object.
3. No Tailscale MCP was discovered — use CLI / Admin API. Prefer MCP when
   ready; **do not invent MCP tool names**.
4. Prefer narrow ACL diffs over rewriting the whole policy file.
5. Never paste auth keys, OAuth client secrets, or API tokens into chat.
6. Cap large device lists; summarize and filter.
7. Neighbor VPN products and cloud firewall craft are out of scope.

## Procedure

1. Decide the surface (devices vs ACLs vs gated mutate). **Done when**
   you can name one surface, or you skipped because none was asked.
2. Resolve tailnet + device/tag ids via status/list/GET (or user paste).
   **Done when** every id you will use was listed/read, or you stopped
   instead of inventing one.
3. Follow the load-map rule (and `tailscale-acl-change` for policy
   edits). Always apply `tailscale-safety` when a mutate is in play.
   **Done when** evidence matches the ask or the mutate was refused.
4. Stop after evidence unless the user also used an implement/mutate
   verb. **Done when** the reply has hostname/tag/policy evidence (no
   keys), and no unauthorized mutate ran.
