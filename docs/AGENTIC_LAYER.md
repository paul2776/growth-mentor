# Agentic Layer — Growth Mentor

## v1: No agentic actions
All v1 actions are direct user CRUD. No agent drafts or executes anything.

## Draftable Actions (later, risk: medium)
| action | trigger | risk | approval |
|---|---|---|---|
| Draft scorecard from reflection text | user submits free-text note | medium | user confirms scores before save |
| Suggest goal re-scoping | 3 weeks avg < 4 on a goal | low | shown as suggestion, user applies |

## Executable After Approval (later, risk: medium)
| action | risk | approval |
|---|---|---|
| Auto-create next week's scorecard | low | auto, logged |
| Mark goal achieved if score = 10 two weeks | medium | user confirms |

## Human-Only (always)
| action | risk |
|---|---|
| Delete a goal | critical — human only |
| Delete vision | critical — human only |
| Delete scorecard history | critical — human only |

## Named Tools (later)
- `parse_reflection(text) → entries[]` — AI, medium risk
- `compute_week_metrics(scorecard_id) → metrics` — deterministic, low risk
- `suggest_rescope(goal_id)` — AI, low risk

No raw `run_any` / `send_any` exposed.

## Audit Log Fields (when added)
`id, actor (user/agent), action, target_type, target_id, risk_level, approved_by, created_at`