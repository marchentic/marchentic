---
name: vaultwarden-audit
description: >-
  Vaultwarden admin audit checklist (users/orgs/config flags; no vault
  secret dumps).
---

# /vaultwarden-audit

1. If the user did not ask for a Vaultwarden admin audit or access
   review, say so and stop.
2. Load `vaultwarden-admin-audit` and follow its checklist.
3. Always apply `vaultwarden-refuse-leak`. No exports, passwords, or
   admin tokens in chat.
4. Return counts, names, and risk flags only.
