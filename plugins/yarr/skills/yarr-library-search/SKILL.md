---
name: yarr-library-search
description: >-
  Checklist for Sonarr/Radarr/Prowlarr library and search via yarr MCP.
  Resolve ids; prefer read; mutates need explicit verb. Skip when no *arr
  search/library ask.
---

# Yarr library search

## Gate

User asked to find, list, or inspect TV/movies/indexers on Sonarr, Radarr
(incl. 4K), or Prowlarr via yarr MCP. Skip pure qBit queue, Plex sessions,
or Seerr-only request lists.

Always load `yarr-arr` and `yarr-safety`.

## Checklist

1. **Tool** — pick `sonarr`, `radarr`, `radarr_4k`, or `prowlarr` from the
   ask (4K movies → `radarr_4k`). **Done when** one tool is named.
2. **Status** — `service_status`. **Done when** the instance is reachable
   or you reported it down.
3. **Help when needed** — `help` if the read path/op is unclear; do not
   invent routes. **Done when** the next action is a real enum member.
4. **Search / list** — `api_get` or read `op` with modest `page` /
   `page_size`; match the title the user named. **Done when** you have
   hits with ids or a justified miss.
5. **Mutate only if asked** — add/monitor/delete needs an explicit verb
   and resolved id (`yarr-safety`). **Done when** refused or applied.
6. **Receipt** — tool + title/id + finding. **Done when** no secrets in
   the reply.

## Report shape

- Tool name + action
- Title + id (when found)
- One next check (Seerr request, qBit queue, or stop)

