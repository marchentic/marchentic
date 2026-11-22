# yarr

Agnostic *arr / Plex / qBittorrent / Seerr craft via the yarr MCP fleet:
search, status, and gated mutations. Prefer yarr MCP; never invent
instance ids.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `yarr-inventory` | Fleet `service_status` across yarr MCP tools |
| `yarr-arr` | Sonarr / Radarr / Prowlarr library and search craft |
| `yarr-plex` | Plex + Tautulli sessions/stats craft |
| `yarr-qbit` | qBittorrent queue via `qbit_*` tools |
| `yarr-seerr` | Seerr / Overseerr request craft |
| `yarr-safety` | Destructive gates; read/search default |

## Skills

| Skill | Purpose |
| --- | --- |
| `yarr` | Index / gate / procedure |
| `yarr-library-search` | *arr library/search checklist |
| `yarr-download-triage` | qBit queue triage checklist |

## Commands

- `/yarr` → Media fleet via yarr MCP
- `/yarr-queue` → qBit download queue triage

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not this product.
- Site library overlays stay in private `homelab`.

## Diagrams

- [`docs/yarr-workflow.drawio`](docs/yarr-workflow.drawio) — gate → route → *arr / Plex / qBit / Seerr

