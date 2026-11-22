---
name: immich-library-search
description: >-
  Immich search checklist: resolve instance, search albums/assets/people,
  report ids and counts. API only; no Immich MCP discovered.
---

# Immich library search

## Gate

User asked to find photos, albums, or people in Immich. Prefer Immich API
(no Immich MCP discovered). Skip mutate paths.

Always load `immich-library`, `immich-safety`, and skill `immich`.

## Checklist

1. **Connect** — resolve base URL; server-info/health.
   **Done when** instance is reachable or auth failed cleanly.
2. **Query** — translate the ask into album/person/date/filename filters;
   run search/list endpoints.
   **Done when** hits come from API, not guesses.
3. **Report** — cap results; id + name/filename + takenAt/counts.
   **Done when** no media bytes or API keys appear.
4. **Safety** — inventory only unless mutate also authorized.
   **Done when** receipt has no unauthorized delete/share.

## Report shape

- Query summary
- Top hits: id, name/filename, counts/dates
- One next step (open album, gated share, or gated trash)
