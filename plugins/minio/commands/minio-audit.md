---
name: minio-audit
description: >-
  MinIO bucket inventory audit: list, usage, versioning/tags via MCP.
---

# /minio-audit

1. If the user did not authorize a MinIO inventory/audit, say so and stop.
2. Load `minio` and skill `minio-bucket-audit` with rules `minio-buckets` /
   `minio-safety`.
3. Prefer MinIO MCP. Pick swarm vs backup from the ask; never invent bucket
   names.
4. Return namespace + bucket list + config/usage highlights (no access keys)
   and one next check.

