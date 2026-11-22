---
name: kopia-repo-status
description: >-
  Kopia health checklist: repository status, recent snapshot coverage,
  policy and maintenance info via CLI. Skip when no status/health ask.
---

# Kopia repo status

## Gate

User asked whether Kopia is healthy, whether snapshots are recent, or for a
short repository status pass. Prefer `kopia` CLI (no Kopia MCP discovered).
Skip pure single-snapshot get (use `kopia-inventory`) and mutate paths.

Always load `kopia-inventory`, `kopia-safety`, and skill `kopia`.

## Checklist

1. **Connect** — `kopia repository status`.
   **Done when** storage type / connected evidence is captured, or auth
   failure is reported.
2. **Recent snapshots** — `kopia snapshot list` (recent first); note sources
   missing a recent snapshot when the user named expected paths.
   **Done when** each cited source has id + time or explicit "no snapshot".
3. **Policies** — `kopia policy list`; `kopia policy show` on focused paths.
   **Done when** retention/compression hints for those paths are noted or
   step skipped.
4. **Maintenance** — `kopia maintenance info` when age/expiry questions arise.
   **Done when** last-run / schedule hint is present or step skipped.
5. **Safety** — inventory only unless user also authorized mutate.
   **Done when** receipt has no unauthorized snapshot/restore/forget.

## Report shape

- Repo status line (backend type, connected — no credentials)
- Recent snapshots: id, source, time
- Policy / maintenance note for focused paths
- One recommended next step (create snapshot, restore drill, or gated forget)
