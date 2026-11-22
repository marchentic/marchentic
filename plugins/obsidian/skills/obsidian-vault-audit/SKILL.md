---
name: obsidian-vault-audit
description: >-
  Checklist for Obsidian vault inventory and health: list notes, spot
  orphans, broken wikilinks, empty stubs. Prefer MCP or filesystem. Skip
  when no inventory/audit ask.
---

# Obsidian vault audit

## Gate

User asked to inventory the vault, find notes, check broken links, orphans,
duplicate titles, empty stubs, or "what's in this vault." Prefer connected
Obsidian MCP; else filesystem under a resolved root. Skip single-note
authoring (use `obsidian-note-author`) and delete/move without an explicit
verb (`obsidian-safety`).

Always load `obsidian-vault` and `obsidian-safety`.

## Checklist

1. **Vault** — resolve root. **Done when** root is known.
2. **Scope** — whole vault, one folder, or a search string the user named.
   Prefer narrow scope. **Done when** the boundary is explicit.
3. **Inventory** — list titles + relative paths (MCP or file walk of
   `*.md`, skip `.obsidian/` unless asked). Cap the first report; paginate
   or summarize when huge.
   **Done when** a short inventory answers "what's there."
4. **Wikilink health** (when asked or cheap) — sample outbound `[[…]]`
   targets; flag missing notes without inventing replacements.
   **Done when** broken-link candidates are listed as paths/titles.
5. **Orphans / stubs** (when asked) — notes with no inbound links, or
   near-empty bodies — report paths only, no body dumps.
   **Done when** a short list (or "none found") is enough.
6. **Mutate** — do not auto-delete orphans or mass-fix links. Offer a
   next step; wait for an explicit verb.
   **Done when** no unauthorized mutate ran.

## Report shape

- Vault root (short) + scope
- Counts (notes scanned, broken links, orphans) when useful
- Bullet list of relative paths / titles (capped)
- Recommended next action (author, fix link, or gated delete) — no dump
