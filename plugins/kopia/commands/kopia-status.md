---
name: kopia-status
description: >-
  Kopia repository health and recent snapshot coverage via CLI.
---

# /kopia-status

1. If the user did not authorize Kopia work, say so and stop.
2. Load skill `kopia-repo-status` (and rules `kopia-inventory`, `kopia-safety`).
3. Run the status checklist; inventory only unless mutate was also authorized.
4. Return repo status + recent snapshots + one next step — no passwords.
