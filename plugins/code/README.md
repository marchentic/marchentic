# code

Coding standards and coding workflow for Claude Code, Cursor, GitHub Copilot,
and OpenAI Codex.

This plugin owns file-type conventions, the always-on smallest-complete-change
ladder, refactor / debug / verify / audit / debt / safety skills, and coding
agents. Tracker filing, git-host craft, product briefs, and a full security
checklist are out of scope. Stack rules keep one-line trust-boundary controls;
`code-workflow` Finish runs a security checklist when available on
trust-boundary diffs, otherwise stops on the local trust-boundary list.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `code-smallest-change` | Always-on lean ladder, never-cut list, skip/risk reply close |
| `code-python` | Python style, typing, Google docstrings, tests |
| `code-javascript` | JavaScript and JSX style, JSDoc, robustness, tests |
| `code-typescript` | TypeScript and TSX types, narrowing, and module boundaries |
| `code-go` | Go formatting, errors, context, and tests |
| `code-rust` | Rust ownership, errors, and tests |
| `code-c` | C types, ownership, headers, and tests |
| `code-cpp` | C++ RAII, types, headers, and tests |
| `code-swift` | Swift optionals, concurrency, modules, and tests (Apple) |
| `code-kotlin` | Kotlin null safety, coroutines, modules, and tests (Android) |
| `code-dart` | Dart / Flutter null safety, widgets, async, and tests |
| `code-java` | Java nullability, exceptions, modules, and tests (Android/JVM) |
| `code-react` | React components, hooks, effects, lists, tests |
| `code-react-native` | React Native platform files, native modules, and tests |
| `code-nextjs` | Next.js App Router / Server vs Client Components |
| `code-flask` | Flask app factory, blueprints, sessions, extensions |
| `code-fastapi` | FastAPI routers, Pydantic, Depends, async |
| `code-html` | Semantic HTML, a11y, safety |
| `code-yaml` | YAML structure, quoting, multi-doc streams, secrets hygiene |
| `code-markdown` | Markdown structure, clarity, safety |
| `code-terraform` | HCL layout, locals SSoT, validation, templates, safety |
| `code-comments` | Sparse durable comments; allows `shortcut:` debt markers |
| `code-unit-testing` | Lasting unit-test philosophy (core contracts, no AI scratch theater); local DB only |
| `code-shell-safety` | Fail-fast shell/Make deletes, rooted refuse, dry-run, WARNING lines |

## Skills (both)

| Skill | Purpose |
| --- | --- |
| `code-workflow` | Intake → execute → verify (ceremony tiers) |
| `code-lean` | Session lean intensity (`lite` / `full` / `ultra`) + command help |
| `code-audit` | Whole-repo / folder quality audit (read-only) |
| `code-safety` | Agent/workspace blast-radius audit (read-only; names/paths only) |
| `code-debt` | Harvest `shortcut:` comments into a ledger |
| `code-investigation` | Evidence-driven codebase investigation |
| `code-systematic-debugging` | Diagnose before fixing |
| `code-verification-before-completion` | Evidence before completion claims |
| `code-deslop` | Dead-path / hygiene cleanup |
| `code-refactor` | Behavior-preserving structure (Python + JS/TS) |
| `code-execute-issue` | Named tracker issue → worktree → open pull request (no merge, not done) |

## Agents (both)

| Agent | Purpose |
| --- | --- |
| `code-technical-lead` | Approach, risks, sequencing |
| `code-reviewer` | Read-only review of a meaningful diff (bug → risk → scale → test → speed → lean) |
| `code-debugger` | Root-cause + minimal fix |
| `code-quality-assurance` | Tests in the same change for app/library code |

## Commands

Primary slash UX (run the matching skill immediately):

- `/code [lite|full|ultra]` → `code-lean` (session lean intensity; bare `/code` reports it)
- `/deslop` → `code-deslop`
- `/refactor` → `code-refactor`
- `/code-review` → launch `code-reviewer`
- `/code-audit` → `code-audit`
- `/code-safety` → `code-safety`
- `/code-debt` → `code-debt`

Also:

- `code-workflow`
- `code-debug`
- `code-investigate`
- `code-verify`
- `/code-execute-issue <ISSUE-KEY>` → `code-execute-issue` (worktree → pull request; manual merge)

Ceremony tiers (Direct / Standard / Full) and lean intensity are orthogonal:
tiers control process; lean controls solution size.

## Docs

- [`docs/code-workflow.drawio`](docs/code-workflow.drawio) — visual map of `code-workflow` (tiers, lean ambient, phases, isolation, subagent routing)
- [`docs/code-workflow.png`](docs/code-workflow.png) — same map, black background
