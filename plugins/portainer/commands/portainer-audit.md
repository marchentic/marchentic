---
name: portainer-audit
description: >-
  Portainer endpoint fleet inventory audit.
---

# /portainer-audit

1. If the user did not authorize Portainer work, say so and stop.
2. Load skill `portainer-endpoint-audit` with rules
   `portainer-endpoints` and `portainer-safety`.
3. Resolve base URL, list endpoints, report type/status (no tokens).
4. Optionally sample stack/container counts on focused endpoints.
