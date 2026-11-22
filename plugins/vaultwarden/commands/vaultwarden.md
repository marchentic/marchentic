---
name: vaultwarden
description: >-
  Vaultwarden admin/ops or user/org inventory with hard refuse to dump
  vault secrets (no Vaultwarden MCP assumed).
---

# /vaultwarden

1. If the user did not authorize Vaultwarden / VW admin work and named
   no user/org/audit ask, say so and stop — unless they asked to dump
   vault contents, then refuse via `vaultwarden-refuse-leak`.
2. Otherwise load `vaultwarden` and follow the matching rule
   (`vaultwarden-ops`, `vaultwarden-users`, `vaultwarden-safety`,
   always `vaultwarden-refuse-leak`). For audits, also follow
   `vaultwarden-admin-audit`.
3. Use Admin API/UI — no Vaultwarden MCP was discovered; do not invent
   MCP tools. Never invent user/org ids.
4. Return names / statuses / counts only — never passwords, TOTP,
   exports, or admin tokens.
