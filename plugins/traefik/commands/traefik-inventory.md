---
name: traefik-inventory
description: >-
  Traefik route inventory: routers/services/middlewares or IngressRoutes.
---

# /traefik-inventory

1. Require an explicit Traefik inventory / “what is routed” ask; else stop.
2. Load skill `traefik-route-inventory` (and skill `traefik` +
   `traefik-safety`).
3. List from manifests, CRs, or confirmed API — never invent names.
4. Report table: name, match, entrypoints, service, TLS, middlewares.
