---
name: grafana-dashboard-author
description: >-
  Checklist for Grafana dashboard author/review: search, summary/panel
  queries, patch or create via update_dashboard, deeplink. Prefer MCP. Skip
  when no dashboard ask.
---

# Grafana dashboard author

## Gate

User asked to find, review, patch, or create a Grafana dashboard or folder.
Prefer connected Grafana MCP. Skip pure Explore query asks (use
`grafana-explore-investigate` / `grafana-explore`).

## Checklist

1. **Search** — `search_dashboards` / `search_folders`. Prefer updating a
   match over minting a near-duplicate title. **Done when** candidates are
   listed or clearly absent.
2. **Read lean** — `get_dashboard_summary` and/or
   `get_dashboard_panel_queries` / `get_dashboard_property` before full
   `get_dashboard_by_uid`. **Done when** panels/queries/variables needed for
   the edit are known.
3. **Datasource UIDs** — resolve panel targets via `list_datasources` /
   existing panel queries; never invent UIDs. **Done when** every datasource
   reference is resolved.
4. **Mutate** — only with an explicit verb (`grafana-safety`). Prefer
   `update_dashboard` patch `operations` for small edits; full `dashboard`
   JSON for new/wholesale. Multi-select in regex: `${var:regex}`. Optional
   `create_folder` when placing a new board. **Done when** MCP returned the
   saved UID, or you refused for lack of verb.
5. **Evidence** — title, UID, folder, change summary, `generate_deeplink`.
   **Done when** reply cites MCP, not guessed URLs.

## Report shape

- Dashboard title / UID / folder
- What changed (panels, queries, variables) or review findings
- Deeplink when available
- Explicit note if mutate was skipped (no verb)
