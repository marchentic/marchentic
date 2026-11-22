---
name: graylog
description: >-
  Agnostic Graylog craft: search logs, streams, and fields via MCP with
  redaction. Prefer Graylog MCP; never invent stream ids; keep secrets out of
  chat. Skip when the user did not authorize this surface.
---

# Graylog

## Gate

No explicit Graylog / log search / stream / field / shipper-to-Graylog ask
and no named stream or Lucene query → **skip**. Prefer a connected Graylog
MCP. Bare product name alone is not enough for a broad dump.

Route by intent:

| Surface | Signals |
| --- | --- |
| Search / context | find logs, errors, Lucene query, message context |
| Aggregate | counts, top sources, percentiles, error rate |
| Streams / fields | list streams, discover fields |
| Incident | outage window, spike, "what broke", correlate errors |
| Shipper | Fluent Bit / Fluentd → Graylog ingestion |

## Load map

| Need | Rule / skill |
| --- | --- |
| Search / context / aggregate / discover | `graylog-search` |
| Incident window → narrow → context | `graylog-search` · skill `graylog-incident-search` |
| Fluent Bit / shipper → Graylog | `graylog-fluent-bit` |
| Redaction / dump refuse | `graylog-safety` (always with the above) |

## Defaults

1. Never invent stream id, index name, or message id — list/resolve first.
2. Bound time ranges; start narrow; expand only after a miss.
3. Prefer `list_streams` / `list_fields` before exotic predicates.
4. Summarize findings; redact secrets (`graylog-safety`).
5. Prefer MCP tools discovered on the live Graylog MCP; do not invent
   tool names.
6. Shipper config stays a thin path — prove ingestion with search, do not
   invent a Fluent Bit plugin.
7. Neighbor metrics / dashboard products are out of scope except as
   context the user already named.

## Procedure

1. Decide the surface (search vs aggregate vs incident vs shipper vs
   discover). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Resolve stream/field ids from MCP (`list_streams`, `list_fields`) or
   from ids the user pasted. **Done when** every id you will use was
   listed/read, or you stopped instead of inventing one.
3. Follow the load-map rule (and `graylog-incident-search` for incident
   windows). Always apply `graylog-safety`. **Done when** the query or
   shipper proof matches the ask and the reply has **no** secret dumps.
4. Stop after a short finding unless the user also asked for a wider
   window or shipper edit. **Done when** the reply has stream/query/time
   + finding (or miss), and no unauthorized broad dump ran.
