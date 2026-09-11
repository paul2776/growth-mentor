# Data Model — Growth Mentor

All tables have: `id uuid PK default gen_random_uuid()`, `created_at timestamptz default now()`, nullable `user_id uuid` (demo-first; FK + RLS added at lock-down).

## visions
| field | type | notes |
|---|---|---|
| id | uuid PK | |
| user_id | uuid nullable | owner scoping later |
| vision_text | text not null | the 10-year statement |
| horizon_years | int default 10 | |
| created_at | timestamptz | |

One row per user (demo: one seeded row).

## pillars
| field | type | notes |
|---|---|---|
| id | uuid PK | |
| name | text not null | Health / Soft Skills / Education / Career & Finance |
| slug | text unique | health, soft-skills, education, career-finance |
| display_order | int | |

Pre-seeded four rows. Read-only in v1.

## goals
| field | type | notes |
|---|---|---|
| id | uuid PK | |
| user_id | uuid nullable | |
| title | text not null | |
| pillar_id | uuid FK→pillars | |
| term | text check in ('long','short') | long = 1–3yr, short = quarterly |
| status | text default 'active' | active / achieved / archived |
| target_date | date nullable | |
| created_at | timestamptz | |

## weekly_scorecards
| field | type | notes |
|---|---|---|
| id | uuid PK | |
| user_id | uuid nullable | |
| week_start_date | date not null | Monday of that week |
| created_at | timestamptz | |

Unique on (user_id, week_start_date). Auto-created on first visit to /scorecard for the current week.

## scorecard_entries
| field | type | notes |
|---|---|---|
| id | uuid PK | |
| scorecard_id | uuid FK→weekly_scorecards | |
| goal_id | uuid FK→goals | |
| score | numeric check 0–10 | self-assessed progress |
| note | text nullable | reflection |
| created_at | timestamptz | |

Unique on (scorecard_id, goal_id).

## RLS (v1)
All tables: RLS enabled. Permissive read/write policies (`using (true)`) so demo works without login. Lock-down sprint replaces with `auth.uid() = user_id`.

## AI fields
None in v1. Future `vision_alignment_score` on goals will carry `value + source + confidence + review_status`.