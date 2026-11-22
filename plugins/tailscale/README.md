# tailscale

Agnostic Tailscale craft — devices, ACLs/grants, and gated key/device/route
changes. Install when Tailscale / tailnet work is in play. No Tailscale MCP
is assumed; craft uses the `tailscale` CLI and Admin API. Headscale and
plain WireGuard stay out of scope.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `tailscale-devices` | Device / status / routes inventory |
| `tailscale-acls` | ACL / grants / tag policy read + minimal craft |
| `tailscale-safety` | ACL widen / keys / device delete / route gates |

## Skills

| Skill | Purpose |
| --- | --- |
| `tailscale` | Index / gate / Procedure |
| `tailscale-acl-change` | Gated ACL change checklist |

## Commands

- `/tailscale` → devices or ACL surface craft (read-first)
- `/tailscale-acl` → ACL review or gated change

## Defaults

- Never invent device, tag, or route ids — list/resolve.
- Read-only inventory is the default; mutates need an explicit verb.
- Transport: `tailscale` CLI / Admin API (prefer a real Tailscale MCP
  later; never invent tool names).
- Prefer minimal ACL diffs over whole-policy rewrites.
- No auth keys, API tokens, or OAuth secrets in chat.

## Diagrams

- [`docs/tailscale-workflow.drawio`](docs/tailscale-workflow.drawio) —
  gate → route devices/ACLs → evidence; mutate refuse branch
