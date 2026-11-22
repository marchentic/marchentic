# traefik

Agnostic Traefik craft: routers, services, middlewares, and IngressRoute
shape with destructive gates. No Traefik MCP discovered — use CRDs, file
provider, Docker labels, or a confirmed API. Never invent router names.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `traefik-routes` | Routers, services, entrypoints, IngressRoute inventory/craft |
| `traefik-middlewares` | Middleware types, attach patterns, chain order |
| `traefik-safety` | Delete / insecure expose / TLS drop / auth-removal gates |

## Skills

| Skill | Purpose |
| --- | --- |
| `traefik` | Index / gate / procedure |
| `traefik-route-inventory` | List routers/IngressRoutes → rule + service + TLS |
| `traefik-ingressroute-author` | Author/patch IngressRoute CRs update-in-place |

## Commands

- `/traefik` → Traefik routes, middlewares, or gated mutate
- `/traefik-inventory` → Route inventory pass
- `/traefik-ingressroute` → IngressRoute author checklist

## Related capabilities

- Other reverse-proxy products and DNS zone edits are out of scope — this
  plugin owns Traefik routing craft only.

## Diagrams

- [`docs/traefik-workflow.drawio`](docs/traefik-workflow.drawio) — gate →
  route → inventory / IngressRoute / middleware-mutate branches
