---
name: traefik
description: >-
  Traefik routers, middlewares, IngressRoute craft, or gated mutate.
---

# /traefik

1. If the user did not authorize Traefik routing work, say so and stop.
2. Load skill `traefik` with rules `traefik-routes`, `traefik-middlewares`,
   and always `traefik-safety`.
3. No Traefik MCP discovered — use CRDs, file provider, Docker labels, or a
   confirmed API base. Never invent router or middleware names.
4. Return name + match/rule + service + entrypoints + TLS state (read) or
   action + object receipt (mutate). For inventory use skill
   `traefik-route-inventory` or `/traefik-inventory`; for IngressRoute
   authoring use `traefik-ingressroute-author` or `/traefik-ingressroute`.
