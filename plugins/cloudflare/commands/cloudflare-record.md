---
name: cloudflare-record
description: >-
  Create or update a Cloudflare DNS record via MCP with safety gates.
---

# /cloudflare-record

1. Require an explicit create/point/update ask; else stop.
2. Load skill `cloudflare-record-change` (and skill `cloudflare` +
   `cloudflare-dns` + `cloudflare-safety`).
3. List first; prefer update-in-place; no API tokens in chat.
4. Receipt: FQDN + type + content (+ ttl/proxied).
