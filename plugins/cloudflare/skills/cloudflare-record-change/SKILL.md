---
name: cloudflare-record-change
description: >-
  Create or update a Cloudflare DNS record via MCP: list first, prefer
  update-in-place, apply safety gates. Skip pure inventory or delete-only.
---

# Cloudflare record change

## Gate

User asked to create, point, or update a Cloudflare DNS record. Skip
list-only (`cloudflare-dns-inventory`) and delete-only (apply
`cloudflare-safety` + `delete_dns_record`).

Always load `cloudflare-dns`, `cloudflare-safety`, and skill `cloudflare`.

## Checklist

1. **Name type content** — from ask; MX needs priority.
   **Done when** type + name + content are fixed (priority if MX).
2. **List first** — `list_dns_records` with `name` (+ `type` when known).
   **Done when** duplicate/existing rows are known.
3. **Update vs create** — if same name/type exists, prefer
   `update_dns_record` with evidenced `recordId` and preserve ttl/proxied
   unless overridden. Else `create_dns_record`.
   **Done when** one mutate tool ran with explicit verb, or you stopped.
4. **Verify** — `get_dns_record` or filtered list.
   **Done when** receipt shows FQDN + type + content (+ ttl/proxied), no
   tokens.
5. **Apex/mail** — if apex/MX/TXT mail-related, blast radius stated before
   mutate. **Done when** risk was stated or N/A.
