---
name: obsidian
description: >-
  Agnostic Obsidian vault craft: note inventory, Markdown/wikilink/frontmatter
  authoring, and gated delete/move. Prefer MCP when connected; otherwise vault
  filesystem. Skip when the user did not authorize this surface.
---

# Obsidian

## Gate

No explicit Obsidian / vault / note / wikilink / frontmatter / `.md` vault ask
→ **skip**. Ordinary repo Markdown that is not an Obsidian vault stays ordinary
coding. Prefer a connected MCP; else the vault filesystem with a resolved root.
Bare "Markdown" alone is not enough.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory / audit | list notes, find orphans, broken links, vault health |
| Author / edit | create note, edit body, frontmatter, wikilinks |
| Mutate | delete, move, rename, bulk retag, purge trash |
| Config | `.obsidian/` settings / plugins (explicit only) |

## Load map

| Need | Rule / skill |
| --- | --- |
| Resolve vault · list/search · author Markdown | `obsidian-vault` · skill `obsidian-note-author` |
| Inventory / orphan / broken-link audit | `obsidian-vault` · skill `obsidian-vault-audit` |
| Delete / move / rename / bulk rewrite gates | `obsidian-safety` |

## Defaults

1. Never invent note paths, folder names, or vault roots — resolve first
   (user path, workspace vault, `.obsidian/` marker, or MCP).
2. Prefer edit-in-place over recreate; preserve existing frontmatter keys the
   user did not ask to change.
3. Use Obsidian wikilinks (`[[Note]]`, `[[Note#Heading]]`, `[[Note|alias]]`)
   and `![[embed]]` when linking inside the vault; use standard Markdown links
   only when the target is outside the vault.
4. Keep YAML frontmatter valid; do not invent community-plugin-only keys unless
   the vault already uses them.
5. Never paste vault secrets, API tokens, or private journal dumps into chat —
   summarize and cite paths (`obsidian-safety`).
6. Destructive acts need an explicit verb naming the object(s).
7. Do not invent MCP tool names — discover live tools or use the filesystem.

## Procedure

1. Decide the surface (inventory/audit vs author vs mutate vs config).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve the vault root and any note paths (MCP or filesystem +
   `.obsidian/` marker). **Done when** every path you will use was listed
   or user-named, or you stopped instead of inventing one.
3. Follow the load-map rule (and compound skill for author or audit).
   Apply `obsidian-safety` on any mutate. **Done when** the action matches
   the ask and the reply has **no** vault dump.
4. Stop after a short receipt unless the user also used an explicit
   destructive or bulk verb. **Done when** the reply has relative path(s)
   + what changed (or audit findings), and no unauthorized delete/move ran.
