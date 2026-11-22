---
name: immich-search
description: >-
  Immich album/asset/person search via API.
---

# /immich-search

1. If the user did not authorize Immich work, say so and stop.
2. Load skill `immich-library-search` with `immich-library` and `immich-safety`.
3. Inventory only unless mutate was also authorized.
4. Return capped hits: id + name/filename — no keys or media dumps.
