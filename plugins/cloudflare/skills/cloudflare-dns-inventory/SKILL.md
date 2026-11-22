---
name: cloudflare-dns-inventory
description: >-
  Cloudflare DNS inventory: list_dns_records (filter name/type), optional get,
  report FQDN + type + content. Skip when no inventory ask.
---

# Cloudflare DNS inventory

## Gate

User asked what a name resolves to in Cloudflare, to list records, or for a
short DNS inventory pass. Skip create/update/delete checklists unless also
authorized.

Always load `cloudflare-dns`, `cloudflare-safety`, and skill `cloudflare`.

## Checklist

1. **Filter** — optional `name` and/or `type` from the ask.
   **Done when** filter is set or “whole configured zone list” is intentional.
2. **List** — `list_dns_records`. **Done when** rows come from MCP.
3. **Detail** — optional `get_dns_record` on focused `recordId` values.
   **Done when** each get uses an id from step 2 or user paste.
4. **Safety** — inventory only unless user also authorized mutate.
   **Done when** receipt has no unauthorized create/update/delete.

## Report shape

| name | type | content | ttl | proxied | recordId |
| --- | --- | --- | --- | --- | --- |
