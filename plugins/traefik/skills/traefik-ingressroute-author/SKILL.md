---
name: traefik-ingressroute-author
description: >-
  Author or patch Traefik IngressRoute CRs: resolve CRD group, match,
  services, TLS, middlewares. Prefer update-in-place; apply safety gates.
---

# Traefik IngressRoute author

## Gate

User asked to create, patch, or rewrite a Kubernetes **IngressRoute** (or
equivalent Traefik CR routing object). Skip pure list-only asks (use
`traefik-route-inventory`). Prefer workspace manifests or live CR read
before write.

Always load `traefik-routes`, `traefik-middlewares` when attaching chains,
`traefik-safety`, and skill `traefik`.

## Checklist

1. **Resolve CRD shape** — read an existing IngressRoute or CRD list for
   apiVersion/kind on this cluster/repo. **Done when** group/version is
   evidenced, not invented.
2. **Name + namespace** — from user paste or existing object; never invent.
   **Done when** metadata.name (+ namespace) is fixed.
3. **Match + entryPoints** — Host/Path expression and entrypoints from ask
   or static Traefik config evidence. **Done when** both are written and
   match the user’s host/path intent.
4. **Services** — in-cluster service name + port (or TraefikService) from
   inventory. **Done when** every service ref was listed/described.
5. **TLS** — secret name or certresolver only if asked; do not disable TLS
   without an explicit insecure verb (`traefik-safety`).
   **Done when** TLS block matches the ask or is explicitly omitted.
6. **Middlewares** — attach only named middlewares that exist or are authored
   in the same change set. **Done when** chain order is stated.
7. **Apply** — prefer patch/update-in-place; delete+recreate only with an
   explicit replace/delete verb. **Done when** post-read shows rule +
   service + TLS, no secrets in the receipt.

## Refuse

- Writing IngressRoute YAML that points at a guessed Service
- Opening cleartext-only public entrypoints without an explicit insecure ask
- Pasting TLS private keys or ACME account material into chat
