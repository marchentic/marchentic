# kubernetes

Agnostic Kubernetes craft — portable manifest authoring plus pod/event/log
triage. Install when Kubernetes MCP is available. Site overlays stay in
private site repos.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `kubernetes-manifests` | Manifest craft (YAML floor + shape, labels, probes, images) |
| `kubernetes-triage` | Workload / event status + MCP tool map + symptom tree |
| `kubernetes-logs` | Short log excerpts (tail, previous, redaction) |
| `kubernetes-external-secrets` | ExternalSecret / SecretStore craft (no values in git) |
| `kubernetes-addons` | Load balancer, ingress, Postgres operator, cache portable notes |
| `kubernetes-safety` | Destructive action gates (delete/scale/exec/apply) |

## Skills

| Skill | Purpose |
| --- | --- |
| `kubernetes` | Index / gate / Procedure |
| `kubernetes-incident-triage` | Live incident checklist (status → events → logs) |
| `kubernetes-manifest-review` | Manifest author/review checklist |

## Commands

- `/kubernetes` → live cluster triage (read-first)
- `/kubernetes-manifest` → portable manifest author/review

## Defaults

- Never invent namespace or pod names — list/resolve via MCP.
- Read-only triage is the default; mutates need an explicit verb.
- Metrics / dashboards — out of scope here.
- Secret-provider product craft — out of scope (key names only via ESO).
- Site-specific overlays — private site repos.

## Diagrams

- [`docs/kubernetes-workflow.drawio`](docs/kubernetes-workflow.drawio) —
  gate → triage vs manifest → evidence; mutate refuse branch
