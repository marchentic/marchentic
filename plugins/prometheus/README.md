# prometheus

Agnostic Prometheus craft: discover metrics/labels/targets, PromQL
instant/range queries, and gated TSDB admin via MCP. Prefer Prometheus
MCP; discover before guessing.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `prometheus-discover` | MCP metrics/labels/series/targets/cardinality discovery |
| `prometheus-query` | Instant / range / exemplar PromQL via MCP |
| `prometheus-safety` | Admin confirm gates, cardinality hygiene, redaction |

## Skills

| Skill | Purpose |
| --- | --- |
| `prometheus` | Index / gate / procedure |
| `prometheus-discover-then-query` | Fuzzy surface → discover → bounded query |

## Commands

- `/prometheus` → Prometheus discover, query, or discover-then-query
- `/prometheus-discover` → Discover-then-query checklist

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/prometheus-workflow.drawio`](docs/prometheus-workflow.drawio) — gate → route → discover / query / admin
