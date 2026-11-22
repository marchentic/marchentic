---
name: runpod-endpoint-deploy
description: >-
  Gated RunPod serverless endpoint create/deploy: GPU pools, image/hub repo,
  create-endpoint or deploy-hub-repo, health check. Prefer MCP.
---

# RunPod endpoint deploy

## Gate

User authorized **create** / **deploy** of a serverless endpoint (or hub
deploy) with an explicit verb. Prefer `user-mcp_runpod`. Skip pure inventory
and pod-only lifecycle.

Always load `runpod-inventory`, `runpod-mutate`, `runpod-safety`, and skill
`runpod`.

## Checklist

1. **Catalog** — `list-gpu-types` (use `pool` ids) and `get-capacity` when
   capacity matters; resolve image or `list-hub-repos` for hub deploy.
   **Done when** pool ids and image/repo are explicit.
2. **Cost** — state serverless workers may bill while active; prefer
   scale-to-zero defaults when the user did not ask for always-on.
   **Done when** intent still matches.
3. **Create** — `create-endpoint` or `deploy-hub-repo` per `runpod-mutate`.
   **Done when** MCP returned an endpoint id.
4. **Prove** — `get-endpoint` and optional `endpoint-health`.
   **Done when** receipt has endpoint id + health/status — no secrets.

## Report shape

- endpoint id + name
- gpu pools / image or hub repo
- health / worker hint
- cost note
