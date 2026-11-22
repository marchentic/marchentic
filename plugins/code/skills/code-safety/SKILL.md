---
name: code-safety
description: >-
  Agent and workspace blast-radius audit: test/dev configs aimed at remote
  DBs, recursive deletes, infra destroy flags, prose-only rules, MCP/harness
  bypass, and CI agents with secrets. Read-only; names and paths only — never
  secret values. Use for "is this repo safe for an agent", "env safety
  audit", /code-safety. Not a quality audit (/code-audit) or an app
  trust-boundary review.
---

# Code safety (agent / workspace blast radius)

Audit what an agent or a one-shot script can destroy in this workspace.
Quality (bugs, lean, load) is a different job — use `code-audit` for that.
App trust-boundary depth (auth, injection, crypto) is a different job — use
a security checklist when available.

## Gate

1. **Audit first. Change nothing** until the user explicitly asks to apply
   named in-repo fixes after this report.
2. **Never print secret values** or use any credential. Show env var names,
   key file paths, and config keys only.
3. Apply **only in-repo** fixes when asked. List anything outside the repo
   (accounts, tokens, harness settings, cloud sync) as **manual** steps.
4. For any risky command that must stay, require a runtime **WARNING** in its
   output that names the hazard and its consequence (that cut agent harm more
   than restating a rule).

## 1. Map first

- Scope: what the user names (folder, package, whole repo + local harness
  configs). Default: whole repo plus discoverable agent/MCP config near it.
- Read: README, `.env*` shapes (names only), compose/test DB config, shell
  scripts and Makefiles, terraform/state, CI workflows, `AGENTS.md` / host
  rule files, MCP config files if present in the tree or documented paths.
- Say which surfaces you did not open.

## 2. Check

Work the list. Skip items that cannot apply. Every finding needs a concrete
path (and line when possible).

1. **Test / preview → remote DB.** Test, dev, or preview configs
   (`.env*`, compose, DB setup) pointing at a non-local or production host,
   especially if tests drop, truncate, reset, or migrate it.
   **Fix:** local or container DB; abort in test setup when the host is not
   local/container.

2. **Credentials in reach.** Committed keys, live payment keys, broad-scope
   credential files the shell can read (report **paths and var names only**).
   Is the default cloud/kube context production?
   **Fix (in-repo):** remove committed secrets; add ignore rules.
   **Manual:** rotate, move prod creds out of this user's default context.

3. **Unbounded deletes.** Recursive deletes whose target comes from a
   variable, glob, or link (`rm -rf "$VAR"`, `rmtree`, `rimraf`); scripts
   without fail-fast unset guards; clean of folders that may contain
   symlinks; tests that rewrite `HOME`.
   **Fix:** `${VAR:?}` (or equivalent), `set -euo pipefail`, `realpath` and
   refuse outside the repo root, dry-run that prints target and file count.
   Put the guard in the script — not a shell alias.

4. **Infra one command can destroy.** Databases or stateful resources without
   deletion protection / `prevent_destroy`; stray `*.tfstate` in the tree;
   `auto-approve` / `--force` on agent-reachable scripts; backups the same
   token can delete.
   **Fix:** add protection flags; drop auto-approve from scripts.
   **Manual:** archive stray state; store backups where this token cannot
   delete them.

5. **Prose-only rules.** Rules that exist only as text (`AGENTS.md`, host
   rules: "code freeze", "never", "ask before"). What enforces each one
   outside the model?
   **Fix:** name a real control next to the rule (deny list, read-only role,
   branch protection, required review) and the safe command to run instead
   (e.g. `make test-local`).

6. **Default branch / token power (manual).** Is the default branch
   protected? Can the operator token force-push, delete repos, or create
   public repos?
   **Manual:** required reviews, no force-push, fine-grained token scoped to
   this repo, block public repo creation in the org.

7. **Cloud-synced checkout (manual).** Repo inside iCloud / Dropbox /
   OneDrive; zero-byte or cloud-only placeholders.
   **Manual:** move the repo out of synced folders. In scripts, verify copy
   size before deleting a source; prefer `mv` to copy-then-delete.

8. **MCP / harness surface.** Unpinned servers (`@latest`, `npx -y`),
   unknown hooks (`SessionStart`, etc.), install scripts, permission-bypass
   flags (`--dangerously-skip-permissions`, `--yolo`), hidden Unicode in rule
   files.
   **Fix:** pin versions; remove unknown hooks/servers/skills; strip hidden
   Unicode; prefer read-only tokens where the server only reads.

9. **CI agent on untrusted input.** Workflows that run an AI agent on issues,
   PR comments, or `pull_request_target` while it can see secrets or write
   access.
   **Fix:** least-privilege `permissions:`; keep secrets out of agent jobs;
   avoid `pull_request_target` for agents; do not share caches with release
   jobs.

10. **Auto-approve / fake safety nets (manual).** Full-access agent modes;
    "guards" that live only as shell aliases (test with a non-interactive
    shell).
    **Manual:** turn off bypass for destructive commands; sandbox the agent
    to the project dir; put guards in scripts or harness deny rules.

## 3. Output

Start with `Blast radius focus:` one or two sentences on what this workspace
lets an agent touch.

Then findings ranked by **blast radius**, top 3 first, numbered so the user
can say "fix 1 and 3". At most 15 findings.

Every finding:

```
1. **Short title** (`path:L40-52` or `manual: …`)
   - **Why dangerous:** …
   - **Fix:** … (in-repo or manual)
   - **If we skip it:** …
```

End with:

- `Top 3 by blast radius:` ids only.
- `In-repo fixes:` numbered list (or `none`).
- `Manual steps:` numbered list (or `none`).
- `Warnings owed:` destructive commands that still lack a runtime WARNING
  line naming hazard + consequence.
- `Not checked:` surfaces you skipped.

Nothing found: `Blast radius focus:`, then `No high blast-radius issues in
scope.` and one line on what you checked.

Wait for approval before editing.
