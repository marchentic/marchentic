---
name: google-cloud
description: >-
  Agnostic Google Cloud craft: project resolution, Compute/GKE inventory,
  Cloud Storage, IAM/network reads, and hard gates on delete/IAM/public ACL.
  Use authenticated gcloud (no Cloud MCP discovered). Skip when the user did
  not authorize GCP work.
---

# Google Cloud

## Gate

No explicit Google Cloud / GCP / gcloud / Cloud Console / project / GCS /
Compute / GKE / IAM / VPC ask and no named project id → **skip**. Prefer a
connected Google Cloud MCP when one exists; otherwise authenticated
`gcloud`. Bare product name alone is not enough.

Route by surface:

| Surface | Signals |
| --- | --- |
| Projects | project id, `gcloud config`, billing link, enabled APIs |
| Compute / GKE | VM, disk, MIG, GKE cluster, node pool |
| Storage | GCS bucket, object, storage class, bucket IAM |
| IAM / network | SA, IAM binding, VPC, firewall, routes, addresses |
| Risk / mutate | delete, public ACL, SA key, broad IAM, open firewall |

## Load map

| Need | Rule / skill |
| --- | --- |
| Project / resource inventory | `google-cloud-inventory` |
| Compute Engine / GKE list-describe | `google-cloud-compute` |
| Cloud Storage buckets / objects | `google-cloud-storage` |
| IAM / VPC / firewall | `google-cloud-iam-network` |
| Incident-style inventory walkthrough | skill `google-cloud-incident-inventory` |
| Delete / IAM / public ACL / keys | `google-cloud-safety` |

## Defaults

1. Never invent project id, zone, region, cluster, bucket, SA email, or
   firewall name — list/resolve first.
2. Read-only inventory is the default. Mutate only with an explicit verb
   naming the resource.
3. No Google Cloud MCP was discovered — use `gcloud` / `gcloud storage`.
   Prefer MCP when ready; **do not invent MCP tool names**.
4. This plugin owns GCP control-plane surfaces (projects, Compute/GKE,
   GCS, IAM/network gates). Workspace mail/docs and in-cluster pod triage
   are out of scope.
5. No service-account keys, OAuth tokens, or full IAM dumps in chat —
   land long-lived secrets in the project’s secret store when asked.
6. State project + location in receipts. Cap large listings.

## Procedure

1. Decide the surface (inventory vs compute/GKE vs storage vs IAM/network
   vs gated mutate). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Resolve project (and zone/region/location) via `google-cloud-inventory`
   before touching resources. **Done when** every id you will use was
   listed/described, or you stopped instead of inventing one.
3. Follow the load-map rule (and `google-cloud-incident-inventory` when the
   ask is a live outage / “what’s wrong in this project”). **Done when**
   status matches the ask or safety refused an unauthorized mutate.
4. Stop after evidence unless the user also used an implement/mutate verb
   that passes `google-cloud-safety`. **Done when** the reply has project +
   resource evidence (no credentials), and no unauthorized mutate ran.
