# runpod

Agnostic RunPod craft: pod/endpoint/template/GPU inventory and gated
create/start/stop/delete via `user-mcp_runpod`. Discover-first; cost-aware;
keep API keys and registry passwords out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `runpod-inventory` | List/get pods, endpoints, templates, GPUs, volumes, billing |
| `runpod-mutate` | Gated create/update/lifecycle/delete via MCP |
| `runpod-safety` | Read-only default, cost gates, secret refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `runpod` | Index / gate / procedure |
| `runpod-pod-lifecycle` | Resolve → cost note → start/stop/delete → get-pod |
| `runpod-endpoint-deploy` | GPU pools → create/deploy → health |

## Commands

- `/runpod` → RunPod inventory or gated craft
- `/runpod-pod` → Gated pod lifecycle checklist
- `/runpod-endpoint` → Gated endpoint deploy checklist

## Related capabilities

- Other GPU clouds and local CUDA debugging are out of scope — this plugin
  owns RunPod surfaces via `user-mcp_runpod` only.

## Diagrams

- [`docs/runpod-workflow.drawio`](docs/runpod-workflow.drawio) — gate → route →
  inventory / pod lifecycle / endpoint-mutate branches
