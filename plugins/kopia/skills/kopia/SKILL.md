---
name: kopia
description: >-
  Agnostic Kopia craft: repository and snapshot inventory plus gated
  snapshot/restore/forget via CLI. No Kopia MCP discovered — do not invent
  tools. Skip when the user did not authorize this surface.
---

# Kopia

## Gate

No explicit Kopia / snapshot / repository backup ask (and no named snapshot
id or repo config on this surface) → **skip**. Bare "back up" without Kopia
is out of scope. Other backup products (including cluster-backup controllers)
are out of scope — do not absorb them here. Prefer `kopia` CLI against a
resolved repository config; use a Kopia MCP only when one is connected — never
invent MCP tool names.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list snapshots, policies, repo status |
| Status | repo health, recent snapshot coverage, maintenance info |
| Snapshot create | create snapshot of a named path |
| Restore | restore snapshot to a destination |
| Forget / maintain | forget snapshots, expire via maintenance |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / status repo, snapshots, policies | `kopia-inventory` |
| Snapshot / restore / forget / maintain | `kopia-mutate` |
| Repo health / recent coverage sweep | skill `kopia-repo-status` |
| Restore run checklist | skill `kopia-restore-run` |
| Gates, restore risk, refuse credentials | `kopia-safety` (always) |

## Defaults

1. Never invent repository path, snapshot id, or policy path — list/resolve first.
2. No Kopia MCP discovered — use authenticated `kopia` CLI; do not invent MCP tools.
3. Resolve repo config from operator config/env — never invent credentials.
4. Read inventory before any mutate (`kopia-inventory`).
5. Restores are data-loss / overwrite shaped — state destination impact.
6. Non-Kopia backup products are out of scope.

## Procedure

1. Decide the surface (inventory / status / snapshot / restore / forget).
   **Done when** you can name one surface, or you skipped because none was asked.
2. Resolve config and names from CLI lists or user paste; never invent.
   **Done when** every path/id used in gets or mutates was listed/read this turn.
3. Follow the load-map rule and compound skill when status or restore run
   is in play. Always apply `kopia-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: snapshot id + source + time (inventory), or
   action + path/DEST + outcome (mutate). **Done when** evidence is cited
   and overwrite risk was stated for restores — no passwords or keys.
