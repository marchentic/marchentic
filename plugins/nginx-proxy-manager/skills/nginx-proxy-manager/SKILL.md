---
name: nginx-proxy-manager
description: >-
  Agnostic Nginx Proxy Manager craft: proxy hosts, SSL certificates, and
  access lists with destructive gates. No NPM MCP discovered — use product
  API or UI. Skip when unauthorized.
---

# Nginx Proxy Manager

## Gate

No explicit Nginx Proxy Manager / NPM / proxy host / SSL cert / access list
ask → **skip**. Other reverse-proxy products are out of scope — do not absorb
them here. Prefer operator-resolved API base URL or admin UI; if an NPM MCP
appears later, use it without inventing tool names.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list hosts, redirections, streams, certs, access lists |
| SSL issue | Let’s Encrypt / DNS-01 / upload cert |
| Access lists | clients, auth, widen/tighten |
| Mutate / risk | delete, disable, retarget upstream, cert wipe |

## Load map

| Need | Rule / skill |
| --- | --- |
| Proxy hosts / redirections / streams | `nginx-proxy-manager-hosts` |
| SSL certificates | `nginx-proxy-manager-ssl` |
| Access lists | `nginx-proxy-manager-access` |
| Host inventory checklist | skill `nginx-proxy-manager-host-inventory` |
| Cert issue checklist | skill `nginx-proxy-manager-ssl-issue` |
| Delete / disable / widen / cert wipe | `nginx-proxy-manager-safety` (always) |

## Defaults

1. Never invent proxy-host, certificate, or access-list ids — list/resolve
   first.
2. No NPM MCP discovered — use REST API or UI on an operator-resolved base
   URL. Prefer MCP when ready; **do not invent MCP tool names**.
3. Never hardcode the NPM instance URL; resolve from config/env/ask.
4. Prefer update-in-place over delete+recreate.
5. Always apply `nginx-proxy-manager-safety` on NPM turns.
6. This plugin owns NPM hosts, SSL, and access lists only.
7. No admin passwords, API tokens, or TLS private keys in chat.

## Procedure

1. Decide the surface (inventory / SSL / access / gated mutate).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve `BASE` and object ids from config/API/UI or user paste; never
   invent. **Done when** every id used was listed/read this turn.
3. Follow the load-map rule and compound skill when inventory or SSL issue
   is in play. Always apply `nginx-proxy-manager-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: id + domains + forward + ssl/access summary
   (no secrets). **Done when** evidence is cited.
