---
name: code-debt
description: >-
  List every durable shortcut: comment as a debt ledger. One-shot report,
  changes nothing unless the user asks to write the ledger to a file. Use for
  "code debt", "list the shortcuts", "what did we defer", /code-debt.
---

# Code debt ledger

Every deliberate lean shortcut is marked with a `shortcut:` comment naming its
ceiling and upgrade trigger (see `code-comments`). This collects them into one
ledger so a deferral cannot quietly become permanent.

## Scan

Grep the repo for comment markers, skipping `.git` and everything the
`.gitignore` files ignore:

```text
git grep --exclude-standard -nE '(#|//|/\*) ?shortcut:'
```

Add other comment prefixes if the stack uses them. If the user names their own
marker word (`/code-debt TODO`), grep for that word instead — still only hits
that look like deferrals, not prose about keyboard shortcuts.

Each hit is one ledger row. Skip hits that are not a deferral.

## Output

One row per marker, grouped by file:

`<path>:<line>  ceiling: <…>.  upgrade: <…>.`

Pull ceiling and trigger from `shortcut: <ceiling>; upgrade when <trigger>`.
Want an owner per row too? add `git blame -L <line>,<line> -- <path>`.

Flag rot risk: any marker that names no upgrade path or trigger gets a
`no-trigger` tag — those are the ones that silently rot.

End with: `N markers, M with no trigger.` Nothing found: `No shortcut debt.
Clean ledger.`

## Boundaries

Reads and reports only. Changes nothing unless the user asks to persist the
ledger (for example `CODE-DEBT.md`). One-shot.
