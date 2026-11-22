---
name: vaultwarden
description: >-
  Agnostic Vaultwarden craft: admin/ops posture and user/org inventory with
  hard refuse to dump vault contents or credentials. Prefer Admin API/UI
  (no Vaultwarden MCP discovered). Skip when unauthorized.
---

# Vaultwarden

## Gate

No explicit Vaultwarden / Bitwarden-compatible vault / VW admin / org
user ask → **skip**. HashiCorp Vault asks are out of scope — do not
absorb them here. Prefer a connected Vaultwarden MCP when one exists;
otherwise Admin API/UI with a resolved base URL. Bare product name alone
is not enough for mutates. Any ask to dump passwords/exports → refuse
via `vaultwarden-refuse-leak` (still “in scope” as a refuse, not skip).

Route by surface:

| Surface | Signals |
| --- | --- |
| Ops / diagnostics | instance health, config flags, admin inventory |
| Users / orgs | invites, membership, disable/delete users |
| Leak / dump | export, paste password, show TOTP, data.json |
| Risk / mutate | delete org, revoke sessions, rotate admin token |

## Load map

| Need | Rule / skill |
| --- | --- |
| Admin/ops inventory + non-secret config | `vaultwarden-ops` |
| Users / orgs / invites / roles | `vaultwarden-users` |
| Admin audit checklist | skill `vaultwarden-admin-audit` |
| Leak / export / chat hygiene | `vaultwarden-refuse-leak` (always) |
| Delete / disable / privilege / token rotate | `vaultwarden-safety` |

## Defaults

1. Never invent org, collection, or user ids — list/resolve first.
2. Resolve the instance base URL from config/env — never hardcode a host.
3. No Vaultwarden MCP was discovered — use Admin API/UI. Prefer MCP when
   ready; **do not invent MCP tool names**.
4. Prefer landing secrets in the vault product — **never** paste vault
   item values into chat or commits (`vaultwarden-refuse-leak`).
5. Read-only admin inventory is the default; mutates need an explicit
   verb naming the object (`vaultwarden-safety`).
6. Prefer the user’s own client for reading any cipher plaintext.
7. HashiCorp Vault and other secret backends are out of scope.

## Procedure

1. Decide the surface (ops vs users/orgs vs leak-refuse vs gated
   mutate). **Done when** you can name one surface, or you skipped
   because none was asked (leak asks still run refuse).
2. Resolve base URL + user/org ids via admin list (or user paste).
   **Done when** every id you will use was listed/read, or you stopped
   instead of inventing one.
3. Follow the load-map rule (and `vaultwarden-admin-audit` for audit
   walks). **Always** apply `vaultwarden-refuse-leak`. Apply
   `vaultwarden-safety` when a mutate is in play. **Done when** the
   reply has **zero** vault secret bytes and evidence matches the ask
   (or refuse ran).
4. Stop after non-secret evidence unless the user also used an
   authorized mutate verb. **Done when** the reply has names/statuses
   only, and no unauthorized mutate or dump ran.
