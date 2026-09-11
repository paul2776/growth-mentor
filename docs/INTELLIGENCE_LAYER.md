# Intelligence Layer — Growth Mentor

## Messy Inputs (future)
Free-text weekly reflection → structured scorecard entries. User might type "didn't study much, gym 3x" → system parses into per-goal scores.

## Auto-Structure Schema (future)
```json
{
  "raw_reflection": "didn't study much, gym 3x, led a team meeting",
  "parsed_entries": [
    { "goal_title": "Study 10h/week", "score": 3, "evidence": "didn't study much" },
    { "goal_title": "Gym 4x/week", "score": 7, "evidence": "gym 3x" },
    { "goal_title": "Lead weekly standup", "score": 9, "evidence": "led a team meeting" }
  ],
  "source": "reflection-parser-v1",
  "confidence": 0.78,
  "review_status": "unreviewed"
}
```

## Events to Track
- `scorecard_created` — user opens a new week
- `entry_scored` — individual goal scored
- `goal_status_changed` — active→achieved
- `vision_updated`

## Scoring Rules (v1, rule-based)
| metric | formula |
|---|---|
| weekly average | `avg(entries.score)` rounded 1dp |
| weakest goal | min score entry in current week |
| streak | consecutive weeks with avg ≥ 6 |
| pillar balance | avg score grouped by pillar (flag if any pillar < 4) |

## What Gets Ranked
- Goals by current-week score ascending (weakest first on dashboard)
- Pillars by average score (surface neglected pillars)

## v1 vs Later
**v1:** deterministic aggregation only — average, streak, weakest, pillar balance. **Later:** AI reflection parsing, vision-goal alignment scoring, recommended next actions.