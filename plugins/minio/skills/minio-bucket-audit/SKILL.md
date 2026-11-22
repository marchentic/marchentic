---
name: minio-bucket-audit
description: >-
  Checklist for MinIO bucket inventory: pick swarm vs backup MCP, list
  buckets, usage/admin, then tags/versioning/lifecycle on named buckets.
  Prefer MCP. Skip when no inventory/audit ask.
---

# MinIO bucket audit

## Gate

User asked what buckets exist, for capacity / usage, swarm vs backup
inventory, or a short audit of bucket config. Prefer a connected MinIO
MCP. Skip pure object upload/download (use `minio-object-transfer`) and
delete asks (apply `minio-safety` only after an explicit verb).

Always load `minio-buckets` and `minio-safety`.

## Checklist

1. **Namespace** — pick `user-mcp_minio_swarm` or `user-mcp_minio_backup`
   from the ask; ask once if both could apply.
   **Done when** the namespace is explicit in the plan.
2. **List** — `list_buckets`. **Done when** names come from MCP (or the
   user pasted exact names to focus).
3. **Usage / admin** — optional `get_data_usage_info` and/or
   `get_admin_info` for cluster shape. **Done when** one short capacity
   or health summary exists, or the user only wanted names.
4. **Per-bucket config** — for buckets in scope: `get_bucket_versioning`,
   `get_bucket_tags`, and when useful `get_bucket_lifecycle` /
   `get_bucket_replication`. **Done when** each focused bucket has a
   one-line config note.
5. **Safety** — no access keys; no invented deletes.
   **Done when** the reply is inventory-only unless a create/tag mutate
   was explicitly authorized.
6. **Dual store** — when both MCPs are in scope, repeat steps 2–4 per
   namespace with clear labels. **Done when** each store has its own
   mini-summary or the user scoped one store only.

## Report shape

- MCP namespace
- Bucket list (or focused subset)
- Usage/admin highlight (if gathered)
- Versioning / tag-keys / lifecycle presence per focused bucket
- One recommended next check (object prefix sample, other MCP, or gated
  mutate)

