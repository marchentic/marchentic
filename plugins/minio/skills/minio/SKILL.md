---
name: minio
description: >-
  Agnostic MinIO / S3 craft: buckets, objects, tags, and gated delete via
  MCP. Prefer MinIO MCP (swarm and/or backup); never invent bucket names;
  refuse secret dumps. Skip when the user did not authorize this surface.
---

# MinIO

## Gate

No explicit MinIO / S3-compatible bucket / object ask (or named MinIO MCP
instance in play) → **skip**. Bare “S3 / bucket” for another object store
is out of scope. Prefer a connected MinIO MCP.

Route by intent:

| Surface | Signals |
| --- | --- |
| Buckets | list/create buckets, tags, versioning, lifecycle, replication, usage |
| Objects | list keys, metadata, tags, versions, ask, presign |
| Transfer | upload, download, copy, text-to-object |
| Audit | "what's on the store", capacity, swarm vs backup inventory |
| Mutate risk | delete, overwrite, public ACL, create bucket |

## Load map

| Need | Rule / skill |
| --- | --- |
| Bucket list / create / config / usage | `minio-buckets` |
| Object list / read / transfer / ask | `minio-objects` |
| Bucket inventory checklist | `minio-buckets` · skill `minio-bucket-audit` |
| Upload / download / copy checklist | `minio-objects` · skill `minio-object-transfer` |
| Delete / overwrite / credentials | `minio-safety` (always with the above) |

## Defaults

1. Never invent bucket names or object keys — list/resolve first.
2. Prefer ready MinIO MCP(s): `user-mcp_minio_swarm` and/or
   `user-mcp_minio_backup`. Pick from the ask; ask once if ambiguous.
3. Credentials belong in a secret store or env — not chat.
4. Delete / overwrite / public ACL / create bucket need an explicit verb
   (`minio-safety`).
5. Prefer MCP tools discovered on the live namespace; do not invent tool
   names (including delete tools that are absent).
6. Neighbor backup products, registries, and cluster APIs are out of
   scope — this plugin owns the MinIO object-store surface only.

## Procedure

1. Decide the surface (buckets / objects / transfer / audit / gated
   mutate). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Choose MCP namespace (swarm vs backup) and resolve bucket/key from
   `list_buckets` / `list_bucket_contents` or user-pasted names.
   **Done when** every name you will use was listed/read, or you stopped
   instead of inventing one.
3. Follow the load-map rule (and compound skill for audit or transfer).
   Always apply `minio-safety`. **Done when** the action matches the ask
   and the reply has **no** access keys or secret bodies.
4. Stop after a short receipt unless the user also used an explicit
   destructive or overwrite verb. **Done when** the reply has namespace +
   bucket (+ key) and no unauthorized delete/overwrite ran.

