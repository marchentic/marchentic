---
name: traefik
description: >-
  Agnostic Traefik craft: routers, services, middlewares, and IngressRoute
  shape with destructive gates. No Traefik MCP discovered — use CRDs, file
  provider, Docker labels, or confirmed API. Skip when unauthorized.
---

# Traefik

## Gate

No explicit Traefik / IngressRoute / router / middleware / entrypoint ask →
**skip**. Other reverse-proxy products are out of scope — do not absorb them
here. Prefer checked-in manifests or authorized cluster/API inventory; if a
Traefik MCP appears later, use it without inventing tool names.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list routers, services, middlewares, IngressRoutes |
| IngressRoute author | write/patch Kubernetes IngressRoute CR |
| Middleware | headers, stripPrefix, auth, rate limit, allowlist |
| Mutate / risk | delete, insecure expose, TLS drop, retarget upstream |

## Load map

| Need | Rule / skill |
| --- | --- |
| Routers, services, entrypoints, IngressRoute | `traefik-routes` |
| Middleware craft / attach | `traefik-middlewares` |
| Inventory checklist | skill `traefik-route-inventory` |
| IngressRoute author checklist | skill `traefik-ingressroute-author` |
| Delete / expose / TLS / auth-drop gates | `traefik-safety` (always) |

## Defaults

1. Never invent router, service, middleware, or IngressRoute names —
   list/resolve first.
2. No Traefik MCP discovered — use manifests / CRDs / labels / confirmed API.
   Prefer MCP when ready; **do not invent MCP tool names**.
3. Prefer update-in-place over delete+recreate.
4. Always apply `traefik-safety` on Traefik turns.
5. This plugin owns Traefik routing craft only (routers, middlewares,
   IngressRoute). Neighbor reverse-proxy products are out of scope.
6. No dashboard credentials, ACME account keys, or TLS private keys in chat.

## Procedure

1. Decide the surface (inventory / IngressRoute author / middleware /
   gated mutate). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Resolve names from manifests, CR list, API, or user paste; never invent.
   **Done when** every name used was listed/read this turn.
3. Follow the load-map rule and compound skill when inventory or
   IngressRoute authoring is in play. Always apply `traefik-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: name + rule/match + service + entrypoints +
   TLS state (no secrets). **Done when** evidence is cited.
