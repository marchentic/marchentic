---
name: yarr
description: >-
  Agnostic *arr / Plex / qBittorrent / Seerr craft via the yarr MCP fleet:
  search, status, and gated mutations. Prefer yarr MCP; never invent
  instance ids. Skip when the user did not authorize this surface.
---

# Yarr

## Gate

No explicit *arr / Plex / qBit / Seerr / Tautulli / Overseerr ask and no
named title, request, or torrent → **skip**. Prefer a connected yarr MCP
(`user-mcp_yarr`). Bare "media" alone is not enough for mutates.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | fleet status, which services are up |
| *arr | Sonarr / Radarr / Prowlarr search, library, indexers |
| Plex / Tautulli | sessions, history, libraries |
| qBit | download queue, pause/resume/add/remove |
| Seerr | requests, approve/deny |
| Mutate | delete media, purge queue, profile change, request decision |

## Load map

| Need | Rule / skill |
| --- | --- |
| Fleet / service status | `yarr-inventory` |
| Sonarr / Radarr / Prowlarr | `yarr-arr` · skill `yarr-library-search` |
| Plex / Tautulli | `yarr-plex` |
| qBit queue / torrents | `yarr-qbit` · skill `yarr-download-triage` |
| Seerr / Overseerr requests | `yarr-seerr` |
| Destructive delete / purge / profile / approve | `yarr-safety` |

## Defaults

1. Never invent Sonarr/Radarr/Plex ids, Seerr request ids, or qBit
   torrent hashes — list/resolve first.
2. Read/search is the default; mutations need an explicit verb
   (`yarr-safety`).
3. Prefer MCP tools discovered on the live yarr MCP; do not invent tool
   or action names.
4. Site library classification overlays stay in private `homelab`.
5. Prefer the named qBit/`*arr` instance tool; ask once when ambiguous.
6. Operator replies: service tool + title/id/hash + short finding — no
   API keys or cookies.
7. Neighbor media products not on this MCP are out of scope.

## Procedure

1. Decide the surface (inventory vs *arr vs Plex vs qBit vs Seerr vs
   mutate). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Resolve service tool + ids from MCP (`service_status`, queue/list
   reads) or from ids the user pasted. **Done when** every id/hash you
   will use was listed/read, or you stopped instead of inventing one.
3. Follow the load-map rule (and compound skill for library search or
   download triage). Always apply `yarr-safety` when a mutate is in play.
   **Done when** evidence matches the ask or the mutate was refused for
   lack of verb.
4. Stop after evidence unless the user also used an implement/mutate
   verb. **Done when** the reply has service + id/title + finding or what
   changed, and no unauthorized mutate ran.

