---
name: kopia-restore
description: >-
  Gated Kopia restore checklist: prove snapshot, name DEST, restore via CLI.
---

# /kopia-restore

1. If the user did not authorize a Kopia **restore**, say so and stop.
2. Load skill `kopia-restore-run` with `kopia-inventory`, `kopia-mutate`,
   and `kopia-safety`.
3. Warn overwrite risk; never invent snapshot ids or destinations.
4. Return snapshot id + DEST + outcome — no credentials.
