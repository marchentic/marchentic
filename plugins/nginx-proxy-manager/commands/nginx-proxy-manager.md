---
name: nginx-proxy-manager
description: >-
  NPM proxy hosts, SSL, access lists, or gated mutate.
---

# /nginx-proxy-manager

1. If the user did not authorize Nginx Proxy Manager work, say so and stop.
2. Load skill `nginx-proxy-manager` with rules `nginx-proxy-manager-hosts`,
   `nginx-proxy-manager-ssl`, `nginx-proxy-manager-access`, and always
   `nginx-proxy-manager-safety`.
3. No NPM MCP discovered — use REST API or UI on an operator-resolved base
   URL. Never invent host or certificate ids; never hardcode the instance URL.
4. Return id + domains + forward + ssl/access summary (read) or action +
   object receipt (mutate). For inventory use
   `nginx-proxy-manager-host-inventory` or `/nginx-proxy-manager-inventory`;
   for cert issue use `nginx-proxy-manager-ssl-issue` or
   `/nginx-proxy-manager-ssl`.
