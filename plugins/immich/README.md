# immich

Agnostic Immich craft: library/album/asset inventory, search, and gated
share/delete via Immich API. No Immich MCP discovered — do not invent tools.
Prefer trash over hard delete; keep API keys and media bytes out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `immich-library` | Albums/assets/people/jobs inventory via API |
| `immich-mutate` | Gated trash/delete/share/admin via API |
| `immich-safety` | Read-only default, trash-over-delete, key refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `immich` | Index / gate / procedure |
| `immich-library-search` | Connect → search → capped hits |
| `immich-share-or-delete` | Resolve → warn → share or trash/delete |

## Commands

- `/immich` → Immich inventory or gated craft
- `/immich-search` → Album/asset/person search
- `/immich-share` → Gated share or delete checklist

## Related capabilities

- Nextcloud photo apps and *arr/Plex fleets are out of scope — this plugin
  owns Immich library surfaces via API/UI only.

## Diagrams

- [`docs/immich-workflow.drawio`](docs/immich-workflow.drawio) — gate → route →
  inventory / search / share-delete branches
