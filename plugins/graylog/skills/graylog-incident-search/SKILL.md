---
name: graylog-incident-search
description: >-
  Checklist for Graylog incident log search: bound the window, resolve
  stream, narrow Lucene, aggregate then context. Prefer MCP. Skip when no
  incident or error-spike ask.
---

# Graylog incident search

## Gate

User named an incident, outage window, error spike, "what broke," failed
deploy correlation, or a time-bounded log hunt. Prefer connected Graylog
MCP. Skip pure shipper-config edits (use `graylog-fluent-bit`) and
open-ended browsing with no time or symptom.

Always load `graylog-search` and `graylog-safety`.

## Checklist

1. **Window** — use the incident start/end the user named (`from`/`to`)
   or a short relative `range` around "now." Prefer absolute ISO8601 when
   the window is known. **Done when** the time bound is explicit.
2. **Stream** — `list_streams` (title filter when known) → pick one
   `stream_id`, or search global only when the user said so.
   **Done when** stream id is from MCP or explicitly global.
3. **Fields** — `list_fields` for service/level/source predicates you will
   use. **Done when** every field in the query was discovered or is a
   well-known Lucene default the user named.
4. **Narrow search** — `search_logs` with fielded Lucene
   (`level:ERROR AND …`), small `limit`, optional `fields` list, prefer
   `deduplicate` or `extract_templates` on noisy volumes.
   **Done when** you have hits or a justified empty result.
5. **Aggregate** — `aggregate_logs` with `metrics=count` (and optional
   avg/percentile) + `group_by` (e.g. `source`, `level`, service field)
   to show top offenders. **Done when** one short table answers "where."
6. **Context** — for a decisive hit, `get_log_context` with
   `message_id` + `index` from the search result (never invented).
   **Done when** before/after narrative is summarized, redacted.
7. **Safety** — no credential/PII dumps (`graylog-safety`).
   **Done when** the reply has finding + query + window, secrets redacted.

## Report shape

- Incident window (`from`/`to` or `range`)
- Stream title/id (or "global")
- Lucene query used
- Top groups / error classes (from aggregate or dedupe)
- One redacted excerpt or context summary
- One recommended next check (wider window, sibling stream, or shipper)
