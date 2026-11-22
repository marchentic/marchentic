---
name: tailscale
description: >-
  Tailscale devices or ACL inventory / gated mutate via CLI or Admin API
  (no Tailscale MCP assumed).
---

# /tailscale

1. If the user did not authorize Tailscale / tailnet work and named no
   device, tag, or ACL change, say so and stop.
2. Otherwise load `tailscale` and follow the matching rule
   (`tailscale-devices`, `tailscale-acls`, `tailscale-safety`). For ACL
   edits, also follow `tailscale-acl-change`.
3. Use `tailscale` CLI and/or Admin API — no Tailscale MCP was
   discovered; do not invent MCP tools. Never invent device or tag ids.
4. Return hostname / IP / tag / policy evidence — no auth keys or API
   tokens.
