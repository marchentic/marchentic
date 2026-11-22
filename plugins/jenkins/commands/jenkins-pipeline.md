---
name: jenkins-pipeline
description: >-
  Author or review portable Jenkinsfile / pipeline entrypoints (SCM pickup
  reminder included).
---

# /jenkins-pipeline

1. If the user did not authorize Jenkinsfile / pipeline craft and named no
   pipeline path, say so and stop.
2. Load `jenkins` and prefer skill `jenkins-pipeline-author` with rules
   `jenkins-pipeline` and `jenkins-ci-from-main`.
3. Keep definitions agnostic — credentials ids only; no invented agent
   labels or product-private job graphs.
4. Return paths + dialect + SCM pickup reminder. Do not claim the pipeline
   is live until a build that checked out the new commit succeeds
   (`jenkins-builds` when a verify run was asked).
