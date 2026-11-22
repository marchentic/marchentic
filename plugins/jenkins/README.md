# jenkins

Agnostic Jenkins craft for Claude Code, Cursor, GitHub Copilot, and OpenAI
Codex — build status, console triage, portable Jenkinsfile authoring, and
CI-from-main SCM pickup reminders. Install when the project uses Jenkins
(Jenkins MCP or equivalent). No product-specific job names hard-coded.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `jenkins-builds` | Status / console / queue / nodes / trigger / stop / config gates |
| `jenkins-pipeline` | Agnostic Jenkinsfile / pipeline entrypoints |
| `jenkins-ci-from-main` | Pipeline edits must be on the SCM ref the job builds |

## Skills

| Skill | Purpose |
| --- | --- |
| `jenkins` | Index / gate / Procedure |
| `jenkins-console-triage` | Failing-build console checklist (status → filter → signal) |
| `jenkins-pipeline-author` | Jenkinsfile author/review checklist + SCM pickup |

## Commands

- `/jenkins` → builds, queue, or console triage (read-first)
- `/jenkins-pipeline` → portable Jenkinsfile author/review

## Defaults

- Never invent job fullname, build number, node, or view path — list/resolve.
- Do not claim SUCCESS without a fresh build read.
- Console excerpts stay short and redacted.
- Trigger / stop / config XML writes need an explicit verb.
- Working-tree pipeline edits are invisible until SCM has the commit.

## Diagrams

- [`docs/jenkins-workflow.drawio`](docs/jenkins-workflow.drawio) —
  gate → builds/console vs pipeline → evidence; mutate refuse branch
