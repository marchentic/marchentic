---
name: nginx-proxy-manager-ssl-issue
description: >-
  Issue or renew NPM certificates: resolve domains, provider, attach to host.
  No private keys in chat; apply safety gates.
---

# NPM SSL issue

## Gate

User asked to issue, renew, or attach an SSL certificate in Nginx Proxy
Manager. Skip list-only cert inventory without issue intent (use hosts/
ssl rules). Prefer API or UI on operator-resolved BASE.

Always load `nginx-proxy-manager-ssl`, `nginx-proxy-manager-hosts` when
attaching, `nginx-proxy-manager-safety`, and skill `nginx-proxy-manager`.

## Checklist

1. **Domains** — exact names from ask; confirm DNS aims at NPM for HTTP-01.
   **Done when** SAN list is fixed.
2. **Provider** — HTTP-01 vs DNS-01 vs upload from ask; DNS credentials stay
   in NPM settings, not chat. **Done when** provider is chosen from evidenced
   options.
3. **Issue** — `POST /api/nginx/certificates` (or UI); wait for success
   evidence. **Done when** new/renewed **cert id** is returned.
4. **Attach** — optional host `PUT` with `certificate_id` after host id
   resolve. **Done when** host get shows cert id or attach was not asked.
5. **Refuse** — no PEM private keys, no DNS provider tokens in chat.
   **Done when** receipt has cert id + domains + expiry hint, no secrets.
