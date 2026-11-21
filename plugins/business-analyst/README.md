# business-analyst

Ambient product and planning craft: always-on stay-out / lean-brief gate,
scope pushback, product-sequence plans, and external research. While this
plugin is installed, `business-analyst-baseline` applies on every turn and
auto-engages on unscoped product asks — no slash command required.

Slash commands remain optional force paths for a full brief or plan lock.
This plugin owns briefs and product sequence; implementation continues in
the same turn after a lean brief when assumptions are safe.

No product, host, or site layout belongs in this plugin.

## Rules

| Rule | Purpose |
| --- | --- |
| `business-analyst-baseline` | Always-on ambient stay-out / lean-brief / pushback gate |
| `business-analyst-brief` | Full brief sections and the testable-requirement bar |
| `business-analyst-when` | Planner-depth triggers after the lean or full brief |
| `business-analyst-research` | Gate before searching outside the repo |

## Skills

| Skill | Purpose |
| --- | --- |
| `business-analyst` | Ambient / full brief playbook and routing |
| `business-analyst-planner` | Lock a product-sequence plan |
| `business-analyst-researcher` | Cited external evidence |

## Agents

| Agent | Purpose |
| --- | --- |
| `business-analyst` | Optional full-brief launch (lean brief is default ambient) |
| `business-analyst-planner` | Lock product sequence (not technical approach) |
| `business-analyst-researcher` | External evidence outside the repo |

## Commands

Optional accelerators (ambient path is the default):

- `/business-analyst` → full `business-analyst` brief
- `/business-analyst-plan` → `business-analyst-planner` (and `business-analyst-researcher` only for an external unknown)

## Diagrams

- [`docs/business-analyst-workflow.drawio`](docs/business-analyst-workflow.drawio) — gate → lean ambient brief (same-turn continue) → planner/researcher → later approach
- [`docs/business-analyst-workflow.png`](docs/business-analyst-workflow.png) — same map, black background

## Defaults

- Stay out of already-scoped work; implement without a brief.
- Unscoped product asks get an automatic lean brief + scope pushback.
- At most one blocker question; everything else is a marked assumption.
- Same-turn continue after lean brief when assumptions are safe.
- Technical approach and touch map are a later pass outside this plugin.
- Ticket/page filing is out of scope here.
- If a credential is pasted: do not copy it; say rotate; continue without the value.
