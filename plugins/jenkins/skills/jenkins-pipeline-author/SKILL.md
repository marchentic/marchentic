---
name: jenkins-pipeline-author
description: >-
  Author or review portable Jenkinsfile / pipeline entrypoints against
  jenkins-pipeline and jenkins-ci-from-main. Skip live build-ops-only asks.
---

# Jenkins pipeline author

## Gate

User asked to write, fix, or review a `Jenkinsfile` or pipeline entrypoint
on disk. Skip pure status/console ops (use `jenkins-console-triage` /
`jenkins-builds`).

## Checklist

1. **Scope files** — named `Jenkinsfile` / pipeline paths or globs the user
   pointed at. Match declarative vs scripted already in the repo.
   **Done when** the file set and dialect are explicit.
2. **Portable craft** — load `jenkins-pipeline` (stages, agents, options,
   credentials ids, YAML floor). **Done when** edits match that rule.
3. **Secrets** — no inline tokens/passwords; credentials **ids** only.
   **Done when** no secret values remain in files you touched.
4. **SCM pickup** — apply `jenkins-ci-from-main`: remind which branch the
   job must see; do not claim live until a build checks out that commit.
   **Done when** the reply states the pickup requirement.
5. **Agnostic** — no product-private job graphs, invented agent labels, or
   untrusted `@Library` pins. **Done when** neighboring patterns are reused
   or gaps are listed as questions.
6. **Verify** — editing files ≠ a green build. Trigger/wait only when asked;
   then follow `jenkins-builds`. **Done when** you did not claim SUCCESS
   without a fresh build read.

## Report shape

- Paths edited or reviewed
- Dialect (declarative / scripted / YAML)
- Must-fix vs note findings (with path)
- SCM pickup reminder (which ref must hold the commit)
- Whether a verify build was requested (yes/no)
