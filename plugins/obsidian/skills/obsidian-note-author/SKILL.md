---
name: obsidian-note-author
description: >-
  Checklist for authoring or editing an Obsidian note: resolve vault and
  path, preserve frontmatter, wikilink peers, gated create. Prefer MCP or
  vault filesystem. Skip when no note author ask.
---

# Obsidian note author

## Gate

User asked to create, draft, edit, or restructure a note (body, frontmatter,
wikilinks, embeds) inside an Obsidian vault. Prefer connected Obsidian MCP;
else vault filesystem. Skip pure inventory/audit (use
`obsidian-vault-audit`) and delete/move (use `obsidian-safety`).

Always load `obsidian-vault` and `obsidian-safety`.

## Checklist

1. **Vault** — resolve root (user path → `.obsidian/` workspace → MCP).
   **Done when** root is known, or ask stopped.
2. **Target** — search/list for an existing note before create. Prefer
   edit-in-place when a title/path already matches.
   **Done when** relative path is resolved or a new path is confirmed
   non-colliding.
3. **Frontmatter** — read existing YAML; preserve unknown keys; add only
   keys the user named or siblings already use.
   **Done when** frontmatter stays valid YAML.
4. **Body** — Obsidian Markdown; wikilinks to peers that exist (search
   before linking); embeds only for resolved attachments.
   **Done when** the note answers the ask without inventing peer paths.
5. **Write** — create/update via MCP or filesystem under the vault root.
   **Done when** the file is on disk at the relative path.
6. **Safety** — no dump of private bodies; no delete/move unless verb.
   **Done when** receipt is path + short change summary only.

## Report shape

- Relative path (and folder)
- Created vs edited
- Frontmatter keys touched (names only)
- Wikilinks added that still need targets (if any)
