---
name: business-analyst
description: >-
  Shape problem, outcomes, requirements, and acceptance criteria; route to
  planner or researcher when needed. Use automatically before the first edit
  when the ask is a new capability or has no testable outcome; skip when
  stay-out matches. Slash command optional.
---

# Business analyst

## Gate

Ambient product shaping. When `business-analyst-baseline` Engage matches,
write the lean brief (or full brief on Full-tier / `/business-analyst`)
before the first product-code edit, then **continue the same turn** when
assumptions are safe.

Pause implementation only for one true product-outcome blocker, unclear
multi-subsystem sequence, or when the user forced `/business-analyst` and
asked to stop at the brief.

Skip this skill when `business-analyst-baseline` Stay out matches — implement
immediately.

## Load map

| Need | Load |
| --- | --- |
| Always-on stay-out / engage gate | `business-analyst-baseline` |
| Full brief sections and the quality bar | `business-analyst-brief` |
| Whether to plan at all | `business-analyst-when` |
| Lock a product sequence | `business-analyst-planner` |
| A fact outside this repo | `business-analyst-research`, then `business-analyst-researcher` |
| Technical approach / touch map | a later technical-approach pass |

## Defaults

- One reversible default beats an open question.
- At most one blocker question. Everything else continues.
- Do not invent a tracker project, board, or assignee.
- Do not name a product the user did not name.
- Stakeholders, priority, non-functionals, and success signal may be `none`
  / `not measured` — write the line explicitly (full brief only).

## Procedure

1. Restate the ask in one sentence. **Done when** a reader can see who is
   affected.
2. Check `business-analyst-baseline` Stay out / Engage. **Done when** you
   either exit to implementation or continue here.
3. Scope pushback: challenge missing "done", "and also" extras, and a second
   hidden product outcome. **Done when** extras are Out of scope or the one
   blocker.
4. Write the lean brief (Problem, Outcome, Requirements, Acceptance
   criteria, Out of scope, Assumptions, Open questions ≤1). On Full-tier,
   `/business-analyst`, or still-vague asks, use every section in
   `business-analyst-brief`. **Done when** every requirement has a matching
   check, or you marked the gap as an assumption.
5. If product sequence or acceptance is still unclear (even without the user
   saying "plan"), or the user asked for a plan this turn, hand off to
   `business-analyst-planner`. **Done when** the planner has a locked plan
   or you recorded why a plan is unnecessary.
6. Name the next action: continue implementation this turn with the stated
   assumptions, pause on the one blocker, or lock a plan. **Done when** that
   action is one sentence.

## Deliverable

Lean path: the seven lean sections from the baseline. Full path: every
section in `business-analyst-brief`. Lead the reply with the outcome and
the requirement count.
