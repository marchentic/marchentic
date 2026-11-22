# compose

Agnostic Docker Compose craft: multi-file `COMPOSE_FILE` layout, project-directory
anchors, overlays/profiles, day-to-day ops, stack review, and hard gates on
destructive downs/volume wipes.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `compose-files` | `COMPOSE_FILE` order, project-dir anchor, overlays, env paths, authoring |
| `compose-ops` | `config` / `up` / `ps` / `logs` / pull / pin tags |
| `compose-safety` | `down -v`, volume wipe, prune, secret-dump refuse |

All rules are **agent-requested** (`alwaysApply: false`).

## Skills

| Skill | Purpose |
| --- | --- |
| `compose` | Gate / load map / defaults / procedure |
| `compose-stack-review` | Merge order, pins, health, secret hygiene checklist |

## Commands

- `/compose` → Docker Compose layout, ops, and stack review craft

## Related capabilities

- Neighbor products and surfaces are out of scope for this plugin — stop if
  the ask is not Compose layout or Docker Compose CLI ops.

## Diagrams

- [`docs/compose-workflow.drawio`](docs/compose-workflow.drawio) — gate → route → layout/ops/review → evidence
