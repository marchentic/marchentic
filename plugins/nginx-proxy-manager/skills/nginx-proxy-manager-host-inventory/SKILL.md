---
name: nginx-proxy-manager-host-inventory
description: >-
  NPM host inventory checklist: list proxy hosts/redirections/streams, report
  domain + upstream + SSL + access. Skip when no inventory ask.
---

# NPM host inventory

## Gate

User asked what is proxied, which domain hits which upstream, or for a short
NPM inventory pass. Skip pure cert-issue (use `nginx-proxy-manager-ssl-issue`)
and unauthorized mutate.

Always load `nginx-proxy-manager-hosts`, `nginx-proxy-manager-safety`, and
skill `nginx-proxy-manager`. Load ssl/access rules when those columns matter.

## Checklist

1. **Resolve BASE** — operator config/env/ask. **Done when** base URL is known
   or you stopped instead of hardcoding.
2. **List proxy hosts** — `GET /api/nginx/proxy-hosts` (or UI equivalent).
   **Done when** rows come from evidence.
3. **Optional redirections / streams** — when the ask includes them.
   **Done when** listed or explicitly skipped.
4. **SSL + access columns** — show certificate_id / access_list_id; optional
   name lookup via ssl/access list endpoints.
   **Done when** each focused host has ssl/access summary or “none.”
5. **Safety** — inventory only unless user also authorized mutate.
   **Done when** receipt has no unauthorized delete/disable.

## Report shape

| id | domains | forward | enabled | ssl | access_list |
| --- | --- | --- | --- | --- | --- |
