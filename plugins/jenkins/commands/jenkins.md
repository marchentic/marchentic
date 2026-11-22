---
name: jenkins
description: >-
  Operate on Jenkins builds, queue, or console triage with agnostic craft
  (MCP first).
---

# /jenkins

1. If the user did not authorize Jenkins build/console/ops work and named
   no job or build, say so and stop.
2. Load `jenkins` and prefer skill `jenkins-console-triage` with rule
   `jenkins-builds` when the ask is status, console, queue, trigger, or stop.
3. Prefer Jenkins MCP tools. Never invent job fullnames or build numbers.
4. Return build result + short redacted evidence. Do not trigger, stop, or
   rewrite config unless explicitly asked.
