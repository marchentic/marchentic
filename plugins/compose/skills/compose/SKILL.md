---
name: compose
description: >-
  Agnostic Docker Compose craft: multi-file COMPOSE_FILE layout, project-directory
  anchors, overlays/profiles, day-to-day ops, and hard gates on destructive
  downs/volume wipes. Skip when the user did not authorize Compose work.
---

# compose

## Gate

No explicit Compose / `docker compose` / stack bring-up / overlay / profile /
compose.yaml ask → **skip**. Ordinary app coding does not require this plugin.
Bare “Docker” alone is not enough unless the ask is clearly Compose layout
or stack ops.

Route by intent:

| Surface | Signals |
| --- | --- |
| Layout / author | `COMPOSE_FILE`, overlay, profile, new `compose.yaml`, env paths |
| Ops | `up`, `ps`, `logs`, pull, restart, recreate, exec |
| Review | “review the stack”, merge order, pin audit, health gaps |
| Risk | `down -v`, volume wipe, prune, force data loss |

## Load map

| Need | Rule / skill |
| --- | --- |
| File layout, `COMPOSE_FILE`, project dir, env paths, authoring | `compose-files` |
| `up` / `ps` / `logs` / `config` / pull / pin tags | `compose-ops` |
| Stack review / merge / pin / health checklist | skill `compose-stack-review` |
| `down -v`, volume wipe, prune, secret dumps | `compose-safety` |

## Defaults

1. Resolve the Compose project directory before mutating — never guess.
2. Prefer `docker compose config` (or equivalent) to prove the merge, then act.
3. Pin image tags in Compose; do not silently float on `latest` for shared stacks.
4. Never hand the user `localhost` / `127.0.0.1` in a URL — use a
   machine-reachable host.
5. Read-only status/logs/config is the default; destructive downs need an
   explicit verb (`compose-safety`).
6. Prefer named project (`name:` / `-p`) when multiple stacks share a host.
7. Never dump `.env` or secret values — cite key names only.
8. Own Compose layout and Docker Compose CLI ops only; image publish pipelines
   and remote orchestrators are out of scope.

## Procedure

1. Decide the surface (layout vs ops vs review vs gated destroy).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve project directory + sticky `COMPOSE_FILE` (or explicit `-f` list)
   before mutate. **Done when** the project root and merge list are known, or
   you stopped instead of guessing.
3. Follow the load-map rule (and `compose-stack-review` when reviewing).
   **Done when** `config` succeeds for layout/ops changes, or findings are
   listed for a review-only ask.
4. Stop after evidence unless the user also used a destructive verb that
   passes `compose-safety`. **Done when** the reply has project + services
   (and health or findings), no secret values, and no unauthorized `-v` /
   prune ran.
