# Architecture — Growth Mentor

## Stack
Next.js 14 (app router) · Supabase (Postgres) · Vercel deploy.

## Build Now vs Later
**Now:** vision CRUD, goal CRUD, weekly scorecard create + score, dashboard summary, seed data.
**Later:** login/RLS, AI nudges, trend charts, multi-user isolation, export.

## Key User Flow — Score This Week
1. User opens `/scorecard` → sees current week's card (auto-created if missing)
2. Each active goal renders a 0–10 slider + note field
3. User adjusts score, types note → `saveScorecardEntry` mutation
4. Server upserts `scorecard_entries` row → returns updated scorecard
5. Dashboard widget recomputes average + weakest goal → UI updates
6. Refresh → same state (server-derived)

## Nav Shell
Left sidebar (desktop) with sections: Dashboard · Vision · Goals · Scorecard. Collapses to hamburger on mobile. Current section highlighted.

## Layers
1. **Data layer** (`lib/data/`) — all Supabase reads/writes; typed functions, one file per object.
2. **App logic** (`lib/logic/`) — scorecard auto-creation, dashboard aggregation, pillar constants.
3. **AI module** (`lib/ai/`) — empty stub in v1; later: vision-to-goal alignment scoring.
Core runs fully without AI — all logic is deterministic server-side functions.

## Repo Structure
```
app/
  (dashboard)/page.tsx
  vision/page.tsx
  goals/page.tsx
  scorecard/page.tsx
  layout.tsx
components/
  Sidebar.tsx
  GoalCard.tsx
  ScoreSlider.tsx
  DashboardWidget.tsx
lib/
  data/vision.ts goals.ts scorecards.ts pillars.ts
  logic/scorecard.ts dashboard.ts
  ai/scoring.ts (stub)
supabase/migration.sql
tests/
  scorecard.test.ts
  dashboard.test.ts
```

## Module Map
| Module | Responsibility | Data owned | Build order |
|---|---|---|---|
| `data/pillars` | Provide four pillar constants + seed | pillars table | 1 |
| `data/vision` | Read/edit single vision record | visions | 2 |
| `data/goals` | CRUD goals, filter by pillar/status | goals | 3 |
| `data/scorecards` | Create weekly card, upsert entries | weekly_scorecards, scorecard_entries | 4 |
| `logic/dashboard` | Aggregate current-week metrics | reads scorecards+goals | 5 |
| `components` | UI surfaces for all modules | none | 6 |
| `ai/scoring` | (stub) future vision-goal alignment | none | later |