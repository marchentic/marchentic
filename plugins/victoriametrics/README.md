# victoriametrics

Agnostic VictoriaMetrics craft: discover metrics/labels/series/TSDB,
MetricsQL/PromQL instant/range queries, and alerts/rules inventory via
MCP. Prefer VictoriaMetrics MCP; discover before guessing.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `victoriametrics-discover` | MCP metrics/labels/series/TSDB/alerts discovery |
| `victoriametrics-query` | Instant / range / explain / prettify via MCP |
| `victoriametrics-safety` | Cardinality hygiene and redaction |

## Skills

| Skill | Purpose |
| --- | --- |
| `victoriametrics` | Index / gate / procedure |
| `victoriametrics-discover-then-query` | Fuzzy surface → discover → bounded query |

## Commands

- `/victoriametrics` → VictoriaMetrics discover, query, or discover-then-query
- `/victoriametrics-discover` → Discover-then-query checklist

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/victoriametrics-workflow.drawio`](docs/victoriametrics-workflow.drawio) — gate → route → discover / query / safety
