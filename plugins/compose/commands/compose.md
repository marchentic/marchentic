---
name: compose
description: >-
  Docker Compose layout, ops, stack review, and destructive gates.
---

# compose

1. Load `compose`. Follow the skill gate, load map, and procedure.
2. Resolve project directory + `COMPOSE_FILE` before mutate.
3. For review/audit asks, load `compose-stack-review`.
4. Destructive downs / volume wipes need an explicit verb (`compose-safety`).
5. Report project name, services, and health or findings — never secret values.
