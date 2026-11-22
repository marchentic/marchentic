---
name: cloudflare
description: >-
  Cloudflare DNS craft via user-mcp_cloudflare: list/create/update/delete
  records with hard gates on delete and bulk rewrites. Skip when unauthorized.
---

# Cloudflare

## Gate

No explicit Cloudflare / Cloudflare DNS / Cloudflare record ask → **skip**.
Bare “DNS” without Cloudflare is out of scope. Prefer connected
`user-mcp_cloudflare` (zone-scoped).

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list/get records, what points where |
| Create / update | add record, point name, change TTL/proxied |
| Delete / bulk risk | delete, clean up, point everything |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / get / create / update | `cloudflare-dns` |
| Inventory checklist | skill `cloudflare-dns-inventory` |
| Create/update checklist | skill `cloudflare-record-change` |
| Delete / bulk / apex-mail gates | `cloudflare-safety` (always) |

## Defaults

1. Never invent zone id or record id — list/resolve first.
2. Prefer `user-mcp_cloudflare`; use only live tools (`list_dns_records`,
   `get_dns_record`, `create_dns_record`, `update_dns_record`,
   `delete_dns_record`).
3. Prefer update-in-place over delete+create.
4. Deletes and “point everything at X” need an explicit verb naming targets.
5. Always apply `cloudflare-safety` on Cloudflare turns.
6. This plugin owns Cloudflare **DNS records** only — not WAF/Workers/Tunnels.
7. Report FQDN + type + content after changes (no API tokens in chat).

## Procedure

1. Decide the surface (inventory / create-update / gated delete).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve record ids via `list_dns_records` / `get_dns_record` or user
   paste; never invent. **Done when** every id used was listed/read this
   turn.
3. Follow the load-map rule and compound skill. Always apply
   `cloudflare-safety`. **Done when** actions match the ask and no
   unauthorized mutate ran.
4. Stop with FQDN + type + content (+ ttl/proxied) receipt — no tokens.
   **Done when** evidence is cited.
