---
name: minio
description: >-
  MinIO bucket/object craft via MCP (swarm or backup).
---

# /minio

1. If the user did not authorize MinIO / object-store work, say so and stop.
2. Load `minio` with rules `minio-buckets` / `minio-objects` / `minio-safety`
   as the load map requires.
3. Prefer a ready MinIO MCP (`user-mcp_minio_swarm` or
   `user-mcp_minio_backup`). Never invent bucket or object keys.
4. Return namespace + bucket (+ key) + short finding (no access keys). For
   inventory audits prefer skill `minio-bucket-audit` or `/minio-audit`; for
   upload/download/copy prefer `minio-object-transfer` or `/minio-transfer`.

