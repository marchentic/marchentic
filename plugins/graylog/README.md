# graylog

Agnostic Graylog craft: search logs, streams, and fields via MCP with
redaction. Prefer Graylog MCP; never invent stream ids; keep secrets out of
chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `graylog-search` | MCP search / context / aggregate + streams/fields discovery |
| `graylog-fluent-bit` | Fluent Bit / shipper → Graylog portable hygiene |
| `graylog-safety` | Redact secrets; refuse full private payload dumps |

## Skills

| Skill | Purpose |
| --- | --- |
| `graylog` | Index / gate / procedure |
| `graylog-incident-search` | Time-bounded incident log hunt checklist |

## Commands

- `/graylog` → Graylog search, discover, or aggregate
- `/graylog-incident` → Incident-window search (narrow → aggregate → context)

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.

## Diagrams

- [`docs/graylog-workflow.drawio`](docs/graylog-workflow.drawio) — gate → route → search / incident / shipper
