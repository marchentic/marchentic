---
name: zot-gc
description: >-
  Gated Zot garbage collection.
---

# /zot-gc

1. If the user did not authorize Zot GC, say so and stop.
2. Load skill `zot-gc-run` with rule `zot-safety` (and `zot-repos` /
   `zot-tags` when scoping).
3. Require an explicit gc/prune verb; prefer tag deletes first when that
   answers the ask.
4. Return scope + result (no registry credentials).
