---
name: zot-audit
description: >-
  Zot repository fleet inventory audit.
---

# /zot-audit

1. If the user did not authorize Zot work, say so and stop.
2. Load skill `zot-repo-audit` with rules `zot-repos` and `zot-safety`.
3. Resolve base URL, list repositories, report tag counts (no credentials).
4. Optionally sample tags on focused repositories.
