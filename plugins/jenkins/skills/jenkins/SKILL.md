---
name: jenkins
description: >-
  Agnostic Jenkins craft: watch builds, triage console output, author
  portable Jenkinsfiles, and remind that CI-from-main edits must land on
  the tracked branch. Prefer Jenkins MCP when ready. Skip when the user
  did not authorize Jenkins work.
---

# Jenkins

## Gate

No explicit build / console / queue / node / Jenkinsfile / pipeline ask and
no named job or build → **skip**. Prefer a connected Jenkins MCP when
Jenkins work is in play. Bare product name alone is not enough.

Route by intent:

| Surface | Signals |
| --- | --- |
| Builds / ops | status, watch, trigger, stop, queue, node, view |
| Console triage | console, log, FAILURE, failing stage, test report |
| Pipeline author | Jenkinsfile, declarative/scripted Pipeline, stages |
| SCM pickup | “will CI see this?”, merge to main, multibranch |

## Load map

| Need | Rule / skill |
| --- | --- |
| Status / wait / trigger / stop / queue / nodes | `jenkins-builds` |
| Console / failure slice / test report walkthrough | `jenkins-builds` · skill `jenkins-console-triage` |
| Edit / review Jenkinsfile or pipeline entrypoints | `jenkins-pipeline` · skill `jenkins-pipeline-author` |
| Pipeline live only after merge / push to tracked ref | `jenkins-ci-from-main` |
| Rewrite job or node `config.xml` | `jenkins-builds` refuse unless explicit mutate ask |

## Defaults

1. Never invent job fullname, build number, node, view path, or queue id.
2. Do not claim a build succeeded without a fresh MCP/API read this turn.
3. Console excerpts stay short and redacted — no secrets.
4. Pipeline definitions stay agnostic: no hard-coded product credentials.
5. YAML entrypoints: 2-space indent, quote ambiguous scalars, no secret
   values in the file.
6. Trigger, stop, cancel-queue, and config writes need an explicit verb.
7. Working-tree pipeline edits are invisible until SCM has the commit the
   job checks out.

## Procedure

1. Decide the surface (builds/ops vs console triage vs pipeline author).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve ids from MCP (job fullname, build number, view) or from files
   on disk for Jenkinsfile work. **Done when** every id you will use was
   listed/read, or you stopped instead of inventing one.
3. Follow the load-map rule (and compound skill when triaging console or
   authoring pipeline). **Done when** status/console evidence matches the
   ask, or the Jenkinsfile matches `jenkins-pipeline`.
4. Stop after evidence unless the user also used an implement / trigger /
   mutate verb. **Done when** the reply has job + result or file paths, and
   no unauthorized trigger/stop/config write ran.
