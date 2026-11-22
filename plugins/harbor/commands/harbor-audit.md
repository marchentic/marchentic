---
name: harbor-audit
description: >-
  Harbor project fleet inventory audit.
---

# /harbor-audit

1. If the user did not authorize Harbor work, say so and stop.
2. Load skill `harbor-project-audit` with rules `harbor-projects` and
   `harbor-safety`.
3. Resolve base URL, list projects, report visibility (no tokens).
4. Optionally sample repos/tags on focused projects.
