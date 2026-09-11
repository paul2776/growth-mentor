# Test Plan — Growth Mentor

## v1 Success Scenario
1. Open app (no login) → dashboard loads with seed data visible
2. Navigate to Vision → edit text → save → refresh → text persists
3. Navigate to Goals → see 6 seeded goals across 4 pillars
4. Click "New Goal" → title "Read 2 books this quarter", pillar Education, term short → save
5. Goal appears in list under Education
6. Navigate to Scorecard → current week auto-created → see all active goals with sliders at 0
7. Score "Read 2 books" at 7, note "finished chapter 3" → save
8. Score another goal at 5 → save
9. Refresh → scores and notes persist
10. Navigate to Dashboard → average shows 6.0, weakest goal listed, streak = 1

## Empty States
- Delete all goals → Goals page shows "No goals yet. Create one to get started."
- New week with no entries → Scorecard shows "Score your goals for this week" with sliders at 0
- Dashboard with no entries → all metrics show 0 / "No data yet"

## Error States
- Supabase unreachable → pages show "Couldn't load. Retry button"
- Save fails (network) → form stays populated, toast "Save failed — try again"
- Score out of range → DB rejects, UI shows error (slider enforces 0–10 client-side too)

## Loading States
- Every page shows skeleton/spinner while fetching
- Scorecard save button shows "Saving…" while mutation in flight

## Partial States
- Scorecard with some goals scored, some not → scored ones show value, unscored show 0
- Dashboard with 1 of 4 pillars having goals → balance bar shows 1 populated, 3 empty

## Auth Boundary (post lock-down)
- User A logs in, creates a goal → logs out → User B logs in → cannot see A's goal
- Unauthed visit → redirected to /login