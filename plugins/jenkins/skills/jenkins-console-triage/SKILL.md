---
name: jenkins-console-triage
description: >-
  Checklist for Jenkins console / build failure triage: resolve job, read
  status, filter console, map signal, report. Prefer MCP. Skip when no
  failing build or console ask.
---

# Jenkins console triage

## Gate

User named a failing build, asked for console/log triage, or wants the
cause of a red job. Prefer connected Jenkins MCP. Skip pure Jenkinsfile
authoring (use `jenkins-pipeline-author`).

## Checklist

1. **Job + build** — exact fullname from the user, URL, or
   `query_items` / `get_item`. Build number from the user or last/failed via
   `get_build`. **Done when** fullname + number are known, or ask stopped.
2. **Status** — `get_build` / `get_running_builds`. Note result, duration,
   whether still building. **Done when** you can say FAILURE / UNSTABLE /
   ABORTED / building without guessing.
3. **Parameters / scripts** — when relevant, `get_build_parameters` and
   `get_build_scripts` to see what ran. **Done when** surprise params are
   listed or skipped as unnecessary.
4. **Console slice** — `get_build_console_output` with `pattern` (ERROR,
   FAILURE, Exception, stage name) plus `limit`. Prefer
   `get_build_test_report` for test failures. **Done when** a short
   redacted excerpt supports the cause.
5. **Signal map** — apply `jenkins-builds` common signals (credential,
   agent offline, SCM, compile/test, timeout, OOM). **Done when** one
   primary cause class is named.
6. **Safety** — no stop/retrigger/config rewrite unless explicit
   (`jenkins-builds`). **Done when** the reply is diagnosis + next check,
   not an unauthorized mutate.

## Report shape

- Job fullname + build number
- Result + failing stage or test when known
- One short redacted console / test excerpt
- One recommended next step (fix product, wait for agent, edit pipeline,
  re-run) — product edits need an implement verb
