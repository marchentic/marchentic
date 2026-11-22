# minio

Agnostic MinIO / S3 craft: buckets, objects, tags, and gated delete via
MCP. Prefer MinIO MCP (`user-mcp_minio_swarm` and/or
`user-mcp_minio_backup`); never invent bucket names; keep access keys out of
chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `minio-buckets` | Bucket list/create/config/usage via dual MinIO MCP map |
| `minio-objects` | Object list/read/transfer/ask/presign via MCP |
| `minio-safety` | Delete/overwrite/public-ACL gates; credential refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `minio` | Index / gate / procedure |
| `minio-bucket-audit` | Bucket inventory checklist (swarm vs backup) |
| `minio-object-transfer` | Upload / download / copy checklist |

## Commands

- `/minio` → MinIO bucket/object craft
- `/minio-audit` → Bucket inventory audit
- `/minio-transfer` → Gated object upload/download/copy

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/minio-workflow.drawio`](docs/minio-workflow.drawio) — gate → route → inventory / transfer / gated mutate

