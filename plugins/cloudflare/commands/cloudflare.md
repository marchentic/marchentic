---
name: cloudflare
description: >-
  Cloudflare DNS list/create/update/delete with MCP and destructive gates.
---

# /cloudflare

1. If the user did not authorize Cloudflare DNS work, say so and stop.
2. Load skill `cloudflare` with rules `cloudflare-dns` and always
   `cloudflare-safety`.
3. Prefer `user-mcp_cloudflare`. Never invent record ids; list before mutate.
4. Return FQDN + type + content (read) or action + record receipt (mutate).
   For inventory use `cloudflare-dns-inventory` or `/cloudflare-inventory`;
   for create/update use `cloudflare-record-change` or `/cloudflare-record`.
