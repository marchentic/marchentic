---
name: kopia-restore-run
description: >-
  Gated Kopia restore checklist: prove snapshot id, name DEST, warn overwrite,
  restore via CLI, verify. Skip when only inventory was asked.
---

# Kopia restore run

## Gate

User authorized a **restore** from a Kopia snapshot with an explicit verb.
Prefer `kopia` CLI (no Kopia MCP discovered). Skip when only inventory or
status was asked.

Always load `kopia-inventory`, `kopia-mutate`, `kopia-safety`, and skill
`kopia`.

## Checklist

1. **Resolve snapshot** — `kopia snapshot list` / describe for the named id
   or source path. **Done when** snapshot exists (or user accepts risk if
   describe is incomplete).
2. **Destination** — DEST from the ask; do not invent paths.
   **Done when** target DEST is explicit in the plan.
3. **Risk statement** — warn overwrite impact on live files; cite
   `kopia-safety`. Prefer staging DEST when ambiguous.
   **Done when** user intent still matches restore after the warning.
4. **Restore** — run the restore CLI per `kopia-mutate` for the installed
   binary. **Done when** CLI accepted the restore or reported a clear error.
5. **Prove** — list DEST or report restored path counts.
   **Done when** receipt has snapshot id, DEST, and outcome — no passwords.

## Report shape

- snapshot id + source (pre-restore)
- DEST + outcome (post-restore)
- overwrite warning acknowledged
- no credentials
