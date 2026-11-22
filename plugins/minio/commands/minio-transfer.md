---
name: minio-transfer
description: >-
  MinIO object upload, download, or copy via MCP with overwrite gates.
---

# /minio-transfer

1. If the user did not authorize an object transfer, say so and stop.
2. Load `minio` and skill `minio-object-transfer` with rules `minio-objects` /
   `minio-safety`.
3. Prefer MinIO MCP. Resolve namespace, bucket, and key first; prove local
   paths; gate overwrites.
4. Return namespace + bucket + key (+ path) receipt — no access keys.

