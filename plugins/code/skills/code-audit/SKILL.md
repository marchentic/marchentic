---
name: code-audit
description: >-
  Quality audit of a whole repo or named folder: bugs, security holes, load
  breaks, risky code without tests, slow paths, and what to delete, merge, or
  split. Ranked, each finding explained in plain English. One-shot report,
  changes nothing. Use for "audit this codebase", "review the whole repo",
  "find bloat", "what can I delete", /code-audit.
---

# Code audit

Audit like the senior who just inherited the tree and will be paged when it
breaks. Order of importance: correct, safe, holds under load, tested, fast,
lean. One-shot report — change no code unless the user explicitly asks to
apply fixes after the report.

Agent / workspace blast radius (remote DBs in tests, unbounded deletes,
infra destroy flags, harness bypass) is a different job — use `code-safety`
/ `/code-safety` for that.

## 1. Map first

- Audit what the user names: a folder, a package, or the whole repo.
  Nothing named: the whole repo.
- Read the README, deploy and build config, dependency list, entry points
  (main, routes, handlers, jobs, CLI commands), and the tests.
- Find the expected load: one person running a script, or many users and
  processes at once. Judge scale against that, and say which load you assumed.
- Trace the main flows end to end: where data comes in, what is stored, what
  goes out. Read those paths fully: user input, money, auth, data writes,
  background jobs, anything shared between processes.
- Big repo: go deep where a mistake costs the most, not file by file. Say
  which parts you did not read.

## 2. Look for

1. **Bug:** wrong result, crash, missed edge case, callers that disagree with
   what a function returns, the same rule applied differently in two places.
2. **Risk:** security holes (injection, weak randomness, secrets in code,
   missing checks on user input), data loss (errors swallowed, writes in the
   wrong order, no transaction).
3. **Scale:** fine for one user, wrong for many: check-then-write races, work
   duplicated by every process, growing memory/lists, query-per-item, O(n²),
   per-process state that must be shared.
4. **Missing test:** risky logic (branch, parser, money, security, data writes)
   with no test that fails when it breaks. One good test, not coverage.
5. **Speed:** big slowdowns are problems; small hot-loop wins are suggestions.
6. **Lean:**
   - **delete:** dead code, unused options/flags/config, speculative features
   - **reuse:** two helpers doing the same thing (keep one, name the path)
   - **stdlib / native:** platform or standard library already does it
   - **yagni:** interface with one implementation, factory with one product,
     wrapper that only passes calls through
   - **merge:** near-copies that must change together
   - **split:** one function or class doing several unrelated jobs — by job,
     never by line count

## 3. Check before you report

- Every finding needs a concrete case. No case, no finding.
- Before calling code unused, grep the whole tree for it, including tests,
  fixtures, config, and string or dynamic references.
- A `shortcut:` comment that names its ceiling and trigger is a decision, not
  a finding, unless the expected load already crosses it.
- Propose the smallest fix that works. Prefer deletion. No style taste.

## 4. Output

Start with `What this repo does:` in two or three sentences, and the load you
assumed.

Then findings in three groups, most important first, skip empty groups:
- **Must fix:** bug, security, data loss, breaks at the expected load.
- **Should fix:** risky untested logic, real slowness, duplication, mixed-job
  functions, code that should not exist.
- **Nice to have:** small speed-ups, shorter forms.

Number findings across all groups (user can say "fix 2 and 5"). At most 20
findings; if you left smaller ones out, say how many.

Every finding:

```
2. **Short title** (`path:L40-52`)
   - **What this is:** …
   - **Problem:** …
   - **Fix:** …
   - **If we skip it:** …
```

End with:
- `Verdict:` one line — healthy, or what to fix first.
- `Lean: -N lines, -M dependencies possible.` when lean findings exist.
- `Not checked:` parts you did not read or could not run.

Nothing found: `What this repo does:`, then `Healthy. Nothing to fix.` and one
line on what you checked.
