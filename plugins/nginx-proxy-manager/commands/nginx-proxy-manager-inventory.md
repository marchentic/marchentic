---
name: nginx-proxy-manager-inventory
description: >-
  NPM host inventory: proxy hosts, optional redirections/streams.
---

# /nginx-proxy-manager-inventory

1. Require an explicit NPM inventory / “what is proxied” ask; else stop.
2. Load skill `nginx-proxy-manager-host-inventory` (and skill
   `nginx-proxy-manager` + `nginx-proxy-manager-safety`).
3. Resolve BASE; list from API/UI — never invent ids.
4. Report table: id, domains, forward, enabled, ssl, access_list.
