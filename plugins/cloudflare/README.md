# cloudflare

Cloudflare DNS craft via `user-mcp_cloudflare`: list/create/update/delete
records with explicit destructive gates. Never invent record ids; prefer
update-in-place; no API tokens in chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `cloudflare-dns` | MCP list/get/create/update + craft defaults |
| `cloudflare-safety` | Delete / bulk / apex-mail gates, refuse tokens |

## Skills

| Skill | Purpose |
| --- | --- |
| `cloudflare` | Index / gate / procedure |
| `cloudflare-dns-inventory` | Filtered list → FQDN + type + content |
| `cloudflare-record-change` | List first → update-in-place or create |

## Commands

- `/cloudflare` → DNS inventory or gated mutate
- `/cloudflare-inventory` → List records pass
- `/cloudflare-record` → Create/update checklist

## Related capabilities

- Non-DNS Cloudflare products (WAF, Workers, Tunnels, R2) and other DNS
  providers are out of scope — this plugin owns DNS records only.

## Diagrams

- [`docs/cloudflare-workflow.drawio`](docs/cloudflare-workflow.drawio) — gate →
  route → inventory / record-change / delete branches
