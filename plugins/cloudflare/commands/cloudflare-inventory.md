---
name: cloudflare-inventory
description: >-
  List Cloudflare DNS records via MCP (optional name/type filters).
---

# /cloudflare-inventory

1. Require an explicit Cloudflare DNS inventory ask; else stop.
2. Load skill `cloudflare-dns-inventory` (and skill `cloudflare` +
   `cloudflare-safety`).
3. Call `list_dns_records`; never invent record ids.
4. Report table: name, type, content, ttl, proxied, recordId.
