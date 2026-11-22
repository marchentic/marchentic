---
name: runpod-endpoint
description: >-
  Gated RunPod serverless endpoint create/deploy checklist via MCP.
---

# /runpod-endpoint

1. If the user did not authorize endpoint create/deploy, say so and stop.
2. Load skill `runpod-endpoint-deploy` with `runpod-inventory`, `runpod-mutate`,
   and `runpod-safety`.
3. Resolve GPU pools from `list-gpu-types`; never invent endpoint ids.
4. Return endpoint id + health + cost note — no secrets.
