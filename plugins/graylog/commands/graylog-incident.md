---
name: graylog-incident
description: >-
  Time-bounded Graylog incident log search: narrow, aggregate, context.
---

# /graylog-incident

1. If the user did not authorize an incident / error-spike log hunt, say so
   and stop.
2. Load `graylog` and skill `graylog-incident-search` with rules
   `graylog-search` / `graylog-safety`.
3. Prefer Graylog MCP. Bound the window first; resolve stream; never invent
   message id or index.
4. Return window + stream + query + top findings (redacted) and one next
   check.
