---
name: minio-object-transfer
description: >-
  Checklist for MinIO object upload, download, or copy via MCP: resolve
  namespace and keys, prove local paths, apply overwrite gates. Prefer MCP.
  Skip when no transfer ask.
---

# MinIO object transfer

## Gate

User asked to upload, download, copy, or write text into an object on a
MinIO MCP surface. Prefer connected MinIO MCP. Skip pure bucket inventory
(use `minio-bucket-audit`) and delete without an explicit verb.

Always load `minio-objects` and `minio-safety`.

## Checklist

1. **Namespace** — `user-mcp_minio_swarm` vs `user-mcp_minio_backup` from
   the ask. **Done when** namespace is chosen.
2. **Resolve** — bucket via `list_buckets` or paste; key via
   `list_bucket_contents` (tight `prefix`) or paste.
   **Done when** src/dst names are not invented.
3. **Local path** (upload/download) — `list_allowed_directories`, then
   `list_local_files` when the file is unclear.
   **Done when** `file_path` is under an allowed directory.
4. **Overwrite check** — if destination key may already exist, confirm
   with list/metadata and require an explicit overwrite/replace verb
   before `upload_object`, `text_to_object`, or `copy_object` onto it.
   **Done when** overwrite is authorized or avoided.
5. **Act** — call the matching tool (`upload_object`, `download_object`,
   `copy_object`, or `text_to_object`). Optional `version_id` only from a
   prior versions list. **Done when** the tool succeeded or a clear error
   is reported.
6. **Receipt** — namespace + bucket + key (+ local path / version);
   secrets redacted. **Done when** no access keys appear in chat.
7. **Presign** — if the user asked to share via URL only, prefer
   `get_object_presigned_url` with bounded `expires` instead of upload.
   **Done when** transfer path matches the ask or you declined public ACL.

## Report shape

- MCP namespace
- Direction (upload / download / copy / text-write)
- Bucket + object key (+ version)
- Local path when used
- Overwrite authorized: yes/no/n/a

