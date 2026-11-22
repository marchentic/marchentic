---
name: graylog
description: >-
  Graylog search, streams/fields discovery, or aggregate via MCP.
---

# /graylog

1. If the user did not authorize Graylog / log search work, say so and stop.
2. Load `graylog` with rules `graylog-search` / `graylog-safety`.
3. Prefer Graylog MCP. List streams/fields before inventing predicates;
   never invent stream ids.
4. Return query + time window + short finding (redacted). For incident
   windows, prefer skill `graylog-incident-search` or `/graylog-incident`.
