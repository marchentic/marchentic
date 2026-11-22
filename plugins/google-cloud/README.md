# google-cloud

Agnostic Google Cloud craft — projects, Compute/GKE, Cloud Storage,
IAM/network inventory, and safety gates. Install when GCP / gcloud is in
play. No Google Cloud MCP is assumed; craft uses authenticated `gcloud`.
Workspace mail/docs stay in the workspace product plugin.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `google-cloud-inventory` | Project resolve + list/describe + APIs |
| `google-cloud-compute` | Compute Engine / GKE inventory + gated mutate |
| `google-cloud-storage` | GCS buckets / objects + gated public ACL |
| `google-cloud-iam-network` | IAM / SA / VPC / firewall inventory |
| `google-cloud-safety` | Delete / broad IAM / keys / public / exposure gates |

## Skills

| Skill | Purpose |
| --- | --- |
| `google-cloud` | Index / gate / Procedure |
| `google-cloud-incident-inventory` | Live incident checklist (project → surface → evidence) |

## Commands

- `/google-cloud` → GCP surface craft (read-first)

## Defaults

- Never invent project, zone, cluster, bucket, or SA ids — list/resolve.
- Read-only inventory is the default; mutates need an explicit verb.
- Transport: `gcloud` / `gcloud storage` (prefer a real Cloud MCP later;
  never invent tool names).
- In-cluster pod/event/log triage — out of scope here.
- No SA keys, tokens, or full IAM dumps in chat.

## Diagrams

- [`docs/google-cloud-workflow.drawio`](docs/google-cloud-workflow.drawio) —
  gate → route inventory/compute/storage/IAM → evidence; mutate refuse branch
