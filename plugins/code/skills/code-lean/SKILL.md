---
name: code-lean
description: >-
  Set or report lean intensity (lite / full / ultra) for the smallest-complete-
  change ladder, or show a quick reference for lean coding commands. Use when
  the user says /code, lite, ultra, "be leaner", or asks how lean mode works.
argument-hint: "[lite|full|ultra]"
---

# Lean intensity

The always-on ladder lives in `code-smallest-change`. This skill only switches
or reports **lean intensity** for the rest of the conversation. It does not
change ceremony tiers (Direct / Standard / Full).

## Arguments

| Arg | Effect |
| --- | --- |
| _(none)_ | If intensity was never set this chat, report `full` (default). If already set, report the current level. |
| `lite` | Build what was asked; name the smaller option in one line. |
| `full` | Apply the full ladder (default). |
| `ultra` | Before building, push back on any *solution shape* the need does not justify. Still execute when the ask is clear — do not open interview loops for reversible approach choice. Product briefs for unscoped outcomes stay out of this skill. |
| `help` | Print the quick reference below; do not change level. |

Acknowledge the new level in one short line, then continue the user's real task
if they attached one in the same message.

## Quick reference

| Surface | What it does |
| --- | --- |
| `code-smallest-change` | Always-on ladder + never-cut + skip/risk reply close |
| `/code lite\|full\|ultra` | This skill — session lean intensity |
| `/code-review` | Diff review: bug → risk → scale → test → speed → lean |
| `/code-audit` | Same checks for a folder or whole repo |
| `/code-debt` | Harvest `shortcut:` comments into a ledger |
| `/deslop` | Dead-path / hygiene cleanup after sprawl |
| `/refactor` | Behavior-preserving structure |

Intensity sticks until changed or the conversation ends.
