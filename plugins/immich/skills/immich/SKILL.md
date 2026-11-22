---
name: immich
description: >-
  Agnostic Immich craft: library/album/asset inventory and gated delete/share
  via Immich API. No Immich MCP discovered — do not invent tools. Skip when
  the user did not authorize this surface.
---

# Immich

## Gate

No explicit Immich / photo library / album / asset ask (and no named album
or asset id) → **skip**. Nextcloud photo asks and *arr/Plex stay out of
scope. Prefer Immich REST API with a resolved base URL; use an Immich MCP
only when one is connected — never invent MCP tool names.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list albums, assets, people, jobs |
| Search | find photos by person, album, date, filename |
| Share | create/revoke public share link |
| Delete / trash | trash, permanent delete, empty trash |

## Load map

| Need | Rule / skill |
| --- | --- |
| List libraries / albums / assets / people | `immich-library` |
| Trash / delete / share / admin | `immich-mutate` |
| Search checklist | skill `immich-library-search` |
| Share or delete checklist | skill `immich-share-or-delete` |
| Gates, trash-over-delete, refuse keys | `immich-safety` (always) |

## Defaults

1. Never invent album, asset, or person ids — list/resolve first.
2. No Immich MCP discovered — use authenticated Immich API; do not invent tools.
3. Resolve the Immich base URL from config/env — never hardcode a host.
4. Prefer trash/archive over permanent delete when silence is enough.
5. Never paste API keys or dump original media bytes into chat.
6. Nextcloud / *arr / Plex are out of scope.

## Procedure

1. Decide the surface (inventory / search / share / delete).
   **Done when** you can name one surface, or you skipped because none was asked.
2. Resolve base URL and ids from API lists or user paste; never invent.
   **Done when** every id used was listed/read this turn.
3. Follow the load-map rule and compound skill when search or share/delete
   is in play. Always apply `immich-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: id + name/count (inventory), or action + ids
   (mutate). **Done when** evidence is cited — no keys or media dumps.
