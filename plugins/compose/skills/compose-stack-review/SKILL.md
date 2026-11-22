---
name: compose-stack-review
description: >-
  Review an existing Docker Compose stack for merge order, project-directory
  anchors, image pins, healthchecks, overlays/profiles, and secret hygiene.
  Skip pure bring-up ops without a review ask.
---

# Compose stack review

## Gate

User asked to review, audit, or fix structure of a Compose stack (merge order,
pins, health, overlays). Skip pure “bring it up” / log-tail asks — use the
primary `compose` skill + `compose-ops` instead.

## Checklist

1. **Scope** — named project directory and Compose files (or sticky
   `COMPOSE_FILE`). **Done when** the file set is explicit.
2. **Project directory** — first sticky file anchors the intended root;
   relative `env_file` / volume / build paths resolve. Load `compose-files`.
   **Done when** the anchor is correct or listed as a must-fix.
3. **Merge** — `docker compose config` succeeds; overlay order matches the
   documented contract; no accidental full-stack duplicates. **Done when**
   config is clean or errors are cited with file paths.
4. **Images** — concrete tags/digests for shared services; call out floating
   `latest`. **Done when** pins are listed (ok / finding).
5. **Health & depends_on** — healthchecks exist where `condition:
   service_healthy` is used; failing checks are noted. **Done when** gaps
   are fixed or listed.
6. **Profiles / optionals** — sidecars are profile- or overlay-gated, not
   forever-on by accident. **Done when** optional services are classified.
7. **Secrets** — no committed `.env` values; examples are placeholders only;
   chat stays key-name-only (`compose-safety`). **Done when** no secret
   values remain in git-bound files you touched.
8. **Mutate** — reviewing ≠ `down -v` or prune. Destructive acts need an
   explicit verb + `compose-safety`. **Done when** you did not wipe volumes
   without authorization.

## Report shape

- Project directory + `COMPOSE_FILE` order
- Must-fix vs note findings (with file paths)
- Whether ops mutate was requested (yes/no)
- Health / pin summary (no secret values)
