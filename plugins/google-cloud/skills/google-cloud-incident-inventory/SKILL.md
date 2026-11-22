---
name: google-cloud-incident-inventory
description: >-
  Checklist for live GCP incident inventory: resolve project, then compute
  or GKE or GCS or IAM/network status via gcloud. Skip when no GCP symptom
  was asked.
---

# Google Cloud incident inventory

## Gate

User named a failing project resource, unreachable VM, unhealthy GKE
cluster, missing bucket/object, IAM denial, or “what’s broken in GCP.”
Prefer authenticated `gcloud`. Skip create-only or pure authoring asks
(use the matching craft rule instead).

## Checklist

1. **Project** — user-named or `gcloud config get-value project` /
   `gcloud projects list`. Do not guess prod.
   **Done when** project id is known or ask stopped.
2. **Surface pick** — compute/GKE vs GCS vs IAM/network from the symptom.
   **Done when** one primary surface is named.
3. **Inventory** — list/describe on that surface only:
   - Compute/GKE → `google-cloud-compute` (instances / clusters / node pools)
   - Storage → `google-cloud-storage` (bucket/object metadata)
   - IAM/network → `google-cloud-iam-network` (bindings / firewall / routes)
   **Done when** failing object names come from a fresh list/describe.
4. **Operations / conditions** — when status is unclear, check recent
   operations or cluster conditions (compute operations list; GKE describe
   conditions). **Done when** one primary cause class is named or absent.
5. **Safety** — no delete / broad IAM / public ACL / SA keys / open
   firewall unless explicit (`google-cloud-safety`).
   **Done when** the reply is diagnosis + next check, not an unauthorized
   mutate.
6. **Out of scope handoff** — if the cluster is fine but pods are failing,
   report cluster/location only; in-cluster pod/event/log triage is not
   this plugin’s job.

## Report shape

- Project id (+ region/zone/location when relevant)
- Object + status / condition
- One short evidence line (from describe/list)
- One recommended next step (read-only unless mutate was authorized)
