# Tasks — Growth Mentor

## Sprint 1 — Database + Seed
**Goal:** Full schema live with demo data.
- [ ] Write migration SQL (visions, pillars, goals, weekly_scorecards, scorecard_entries)
- [ ] Enable RLS with permissive v1 policies
- [ ] Seed 4 pillars, 1 vision, 6 goals (mix long/short, all pillars), 3 weeks of scorecards with entries
- [ ] Run migration on Supabase project
**DoD:** Tables exist, seed rows queryable, RLS policies allow anon read/write.

## Sprint 2 — Data Layer + Vision & Goals CRUD
**Goal:** Core objects editable through the UI.
- [ ] `lib/data/` functions for visions, goals, pillars (typed)
- [ ] Vision page: view + edit vision text (inline form)
- [ ] Goals page: list grouped by pillar, create/edit/archive goal
- [ ] Sidebar nav shell (desktop sidebar, mobile hamburger)
- [ ] Loading / empty / error states on both pages
**DoD:** User can edit vision and create/archive a goal; data persists on refresh.

## Sprint 3 — Weekly Scorecard Engine ← v1 functional milestone
**Goal:** The one core engine works end-to-end.
- [ ] `lib/data/scorecards.ts` — create-or-get current week, upsert entry
- [ ] `lib/logic/scorecard.ts` — auto-create current week on visit
- [ ] Scorecard page: list active goals, 0–10 slider + note per goal, save
- [ ] Scorecard history list (past weeks, clickable)
- [ ] Loading / empty / error states
**DoD:** User scores 3 goals this week, refresh shows same scores. ← **v1 works end-to-end here**

## Sprint 4 — Dashboard
**Goal:** Current-week summary visible.
- [ ] `lib/logic/dashboard.ts` — avg score, weakest goal, streak, pillar balance
- [ ] Dashboard page: metric cards + weakest-goals list + pillar balance bar
- [ ] Loading / empty / error / partial (no entries yet) states
**DoD:** After scoring goals, dashboard shows correct average, weakest goal, and streak.

## Sprint 5 — Lock It Down
**Goal:** Real users + per-user isolation.
- [ ] Add Supabase Auth (email/password)
- [ ] Signup / login pages
- [ ] Replace permissive RLS with `auth.uid() = user_id` policies
- [ ] Redirect unauthed users to login (app no longer anonymous)
- [ ] Migrate seed data to a demo user account
**DoD:** Two logged-in users cannot see each other's goals or scorecards.

## Sprint 6 — Intelligence (later)
- [ ] Reflection text → parsed scorecard entries (AI, medium risk, user confirms)
- [ ] Vision-goal alignment score on goals (AI field: value+source+confidence+review_status)
- [ ] Suggested next actions when pillar avg < 4

## Gantt
```
S1 ██████████  DB + Seed
S2 ██████████  Data layer + Vision/Goals CRUD
S3 ██████████  Scorecard Engine  ← v1 functional
S4 ██████████  Dashboard
S5 ░░░░░░░░░░  Lock Down (auth + RLS)
S6 ░░░░░░░░░░  Intelligence
```