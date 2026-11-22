---
name: traefik-route-inventory
description: >-
  Traefik route inventory checklist: list routers/services/middlewares or
  IngressRoutes, then report rule + service + TLS. Skip when no inventory ask.
---

# Traefik route inventory

## Gate

User asked what is routed, which host hits which service, whether a
middleware is attached, or for a short Traefik inventory pass. Skip pure
authoring (use `traefik-ingressroute-author`) and unauthorized mutate.

Always load `traefik-routes`, `traefik-middlewares` when chains are in play,
`traefik-safety`, and skill `traefik`.

## Checklist

1. **Scope** — namespace / provider (CRD vs file vs Docker) / host filter.
   **Done when** one inventory scope is named.
2. **List routers / IngressRoutes** — from manifests, cluster CRs, or
   confirmed API. **Done when** rows come from evidence, not guesses.
3. **Services** — resolve backend refs for focused routers.
   **Done when** each cited router has a service + port from evidence.
4. **Middlewares** — when the ask mentions auth, headers, or allowlists,
   list attached middleware names and types.
   **Done when** chain is shown or explicitly “none attached.”
5. **TLS** — note TLS block / secret name / certresolver **names only**.
   **Done when** TLS state is stated without private key material.
6. **Safety** — inventory only unless user also authorized mutate.
   **Done when** receipt has no unauthorized delete/expose.

## Report shape

| name | match / rule | entrypoints | service | TLS | middlewares |
| --- | --- | --- | --- | --- | --- |

Plus one recommended next step (patch rule, retarget service, or gated
delete) only when the user asked what to do next.
