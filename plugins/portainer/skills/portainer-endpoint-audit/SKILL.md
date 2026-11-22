---
name: portainer-endpoint-audit
description: >-
  Checklist for Portainer endpoint fleet inventory: resolve base URL, list
  endpoints, status/type, then sample stacks/containers on focused
  endpoints. Skip when no inventory/audit ask.
---

# Portainer endpoint audit

## Gate

User asked what endpoints exist, for Portainer fleet health, or a short
audit of environments. Prefer Portainer API/UI (no Portainer MCP in the
live catalog). Skip pure stack deploy (use `portainer-stack-deploy`) and
delete/prune asks (apply `portainer-safety` only after an explicit verb).

Always load `portainer-endpoints` and `portainer-safety`.

## Checklist

1. **Base URL** — from config/env; never hardcode.
   **Done when** the product URL is explicit in the plan (no credentials).
2. **List endpoints** — API/UI environments list.
   **Done when** names/ids come from the live surface or user paste.
3. **Per-endpoint note** — type (Docker / Swarm / K8s) + status.
   **Done when** each focused endpoint has a one-line health note.
4. **Optional sample** — for endpoints in scope, list stack count and/or
   container count via `portainer-stacks` / `portainer-containers` read
   paths. **Done when** the user wanted depth, or you stopped at the
   endpoint list when that was enough.
5. **Safety** — no tokens; no invented deletes.
   **Done when** the reply is inventory-only unless a mutate was
   explicitly authorized.

## Report shape

- Portainer base URL (host only)
- Endpoint list (name / id / type / status)
- Optional stack/container counts per focused endpoint
- One recommended next check (named stack detail, container logs, or
  gated mutate)
