# Product Requirements — Growth Mentor

## Problem
People optimize for incremental gains, staying stuck in safe 2x cycles instead of aiming for 10x potential. Traditional coaches fix this but cost $200–500/session and only offer weekly check-ins. Growth Mentor forces a 10-year vision as the system constraint, then cascades it into weekly measurable actions.

## Target User
The builder and their students — individuals serious about exponential growth across goals, health, soft skills, and education.

## Core Objects
- **Vision** — the 10-year north-star constraint (one per user, editable)
- **Goal** — long-term (1–3 yr) and short-term (quarterly) goals linked to a vision pillar
- **Pillar** — health, soft skills, education, career/finance (categories goals roll up to)
- **WeeklyScorecard** — a week's snapshot: each active goal scored 0–10 on progress + a self-assessment note
- **ScorecardEntry** — one goal's score + note inside a scorecard

## MVP (v1) — Checklist
- [ ] Vision page: view/edit the 10-year vision text
- [ ] Goals page: CRUD long-term & short-term goals, assign pillar
- [ ] Pillars: pre-seeded four pillars, visible on goals page
- [ ] Weekly Scorecard: create this week's scorecard, score each active goal 0–10, add note
- [ ] Scorecard history list with trend sparkline per goal
- [ ] Dashboard: current week summary — average score, weakest goal, streak count
- [ ] All pages render with seed data, no login required

## Non-goals (v1)
- No human coach / peer review loop
- No AI-generated nudges or interventions
- No mobile native app
- No billing or subscriptions
- No social / team accountability features

## Success Criteria (end-to-end)
A user opens the app (no login), edits their 10-year vision, creates one short-term goal under the "Education" pillar, opens this week's scorecard, scores that goal a 7 with a note, and sees the dashboard update to show average score 7 and the goal listed as active — all persisted, reflected on refresh.

## Definition of Done
**PASS:** A user can create a goal, score it in this week's scorecard, and see the updated average on the dashboard — data survives a page refresh. **FAIL:** any dead button, seed-only screen, or lost data.