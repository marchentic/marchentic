# nginx-proxy-manager

Agnostic Nginx Proxy Manager craft: proxy hosts, SSL certificates, and access
lists with destructive gates. No NPM MCP discovered — use product REST API or
admin UI on an operator-resolved base URL. Never invent host ids.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `nginx-proxy-manager-hosts` | Proxy hosts, redirections, streams via API/UI |
| `nginx-proxy-manager-ssl` | Certificate list / issue / attach |
| `nginx-proxy-manager-access` | Access list clients/auth craft |
| `nginx-proxy-manager-safety` | Delete / disable / cert wipe / access-widen gates |

## Skills

| Skill | Purpose |
| --- | --- |
| `nginx-proxy-manager` | Index / gate / procedure |
| `nginx-proxy-manager-host-inventory` | List hosts → domain + upstream + SSL |
| `nginx-proxy-manager-ssl-issue` | Issue/renew cert → optional host attach |

## Commands

- `/nginx-proxy-manager` → Hosts, SSL, access lists, or gated mutate
- `/nginx-proxy-manager-inventory` → Host inventory pass
- `/nginx-proxy-manager-ssl` → Cert issue checklist

## Related capabilities

- Other reverse-proxy products and DNS zone edits are out of scope — this
  plugin owns NPM hosts, SSL, and access lists only.

## Diagrams

- [`docs/nginx-proxy-manager-workflow.drawio`](docs/nginx-proxy-manager-workflow.drawio)
  — gate → route → inventory / SSL / mutate branches
