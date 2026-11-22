---
name: traefik-ingressroute
description: >-
  Author or patch Traefik IngressRoute CRs with safety gates.
---

# /traefik-ingressroute

1. Require an explicit IngressRoute create/patch ask; else stop.
2. Load skill `traefik-ingressroute-author` (and skill `traefik` +
   `traefik-routes` + `traefik-safety`; middlewares when attaching).
3. Resolve CRD apiVersion from evidence; never invent service names.
4. Prefer update-in-place; receipt: name + match + service + TLS (no secrets).
