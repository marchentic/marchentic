---
name: google-cloud
description: >-
  Operate on Google Cloud projects, Compute/GKE, GCS, and IAM/network with
  gated craft (gcloud; MCP only when a real Cloud MCP is ready).
---

# /google-cloud

1. If the user did not authorize Google Cloud / GCP work and named no
   project or resource, say so and stop.
2. Otherwise load `google-cloud` and follow the matching rule
   (`google-cloud-inventory`, `google-cloud-compute`, `google-cloud-storage`,
   `google-cloud-iam-network`, `google-cloud-safety`). For live outages,
   also follow `google-cloud-incident-inventory`.
3. Use authenticated `gcloud` — no Google Cloud MCP was discovered; do not
   invent MCP tools. Never invent project ids.
4. Return project / resource names and short evidence — no credentials,
   tokens, or key material.
