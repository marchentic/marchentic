# vaultwarden

Agnostic Vaultwarden craft — admin/ops posture, user/org inventory, and
hard refuse to dump vault contents or credentials. Install when
Vaultwarden / Bitwarden-compatible admin work is in play. No Vaultwarden
MCP is assumed; craft uses Admin API/UI. HashiCorp Vault stays out of
scope.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `vaultwarden-ops` | Admin/ops inventory + non-secret config flags |
| `vaultwarden-users` | Users / orgs / invites / roles |
| `vaultwarden-refuse-leak` | Hard refuse vault dumps / credential paste |
| `vaultwarden-safety` | Delete / disable / privilege / token gates |

## Skills

| Skill | Purpose |
| --- | --- |
| `vaultwarden` | Index / gate / Procedure |
| `vaultwarden-admin-audit` | Admin audit checklist (no secret dumps) |

## Commands

- `/vaultwarden` → admin/ops or user/org craft (read-first)
- `/vaultwarden-audit` → admin audit walkthrough

## Defaults

- Never invent user, org, or collection ids — list/resolve.
- Read-only admin inventory is the default; mutates need an explicit verb.
- Transport: Admin API/UI (prefer a real Vaultwarden MCP later; never
  invent tool names).
- **Never** dump vault item contents, passwords, TOTP, exports, or admin
  tokens into chat or commits.
- Prefer the user’s own client for reading secrets.
- HashiCorp Vault — out of scope here.

## Diagrams

- [`docs/vaultwarden-workflow.drawio`](docs/vaultwarden-workflow.drawio) —
  gate → route ops/users/audit → evidence; refuse-leak + mutate refuse
  branches
