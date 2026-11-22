---
name: vaultwarden-admin-audit
description: >-
  Checklist for Vaultwarden admin audit: resolve instance, list users/orgs
  metadata, flag risky config — never dump vault item secrets. Skip when
  no admin/audit ask.
---

# Vaultwarden admin audit

## Gate

User asked for a Vaultwarden admin audit, user/org inventory review, or
“who has access / is signup open.” Prefer Admin API/UI (no Vaultwarden
MCP discovered). Skip cipher/item content asks (refuse). Skip pure
invite-create without audit framing (use `vaultwarden-users`).

Always load `vaultwarden-ops`, `vaultwarden-users`,
`vaultwarden-refuse-leak`, and `vaultwarden-safety`.

## Checklist

1. **Authorize** — confirm Vaultwarden admin/audit was asked. **Done
   when** in scope, or you skip.
2. **Base URL** — resolve from operator config/env. **Done when** known
   without inventing a host.
3. **Users** — list users: email, enabled, 2FA boolean if available —
   no secrets (`vaultwarden-users`). **Done when** counts + notable
   anomalies (disabled, pending) are known.
4. **Orgs** — list orgs + member counts / admin roles. **Done when**
   org names and privilege outliers are named.
5. **Config flags** — signup / invitations / SSO flags as booleans only
   (`vaultwarden-ops`). **Done when** risky open-signup (if any) is
   called out without dumping env.
6. **Safety** — no delete/disable/export unless explicit verb
   (`vaultwarden-safety` + refuse-leak). **Done when** reply is
   findings + recommended next check, not an unauthorized mutate.
7. **Receipt** — counts, names, flags — **zero** cipher bytes. **Done
   when** the reply has that shape.

## Report shape

- Instance base (non-secret host the operator already uses)
- User count / org count / pending invites
- One to three risk findings (open signup, org-admins, disabled 2FA
  rate if known)
- One recommended next step (read-only unless mutate authorized)
