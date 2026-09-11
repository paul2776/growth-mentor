# Security — Growth Mentor

## Secrets
Supabase service key lives only in server-side env vars. Never imported in client components. Browser uses anon key with RLS.

## Permission Model
**v1 (demo-first):** RLS enabled, permissive policies (`using (true)`) — app works without login for demo.
**Lock-down (later):** Replace permissive policies with `auth.uid() = user_id` on all tables. Each user sees only their own visions, goals, and scorecards. Until then, treat data as non-sensitive demo content.

## Approved Tools
Only named, typed functions in `lib/data/`. No generic `execute_sql` or `run_any` exposed to the UI or any agent. Each mutation is a specific function (`createGoal`, `upsertEntry`, etc.).

## Agent Permissions (future)
When AI actions land, agent inherits the calling user's permissions — it can only read/write what the user can. Every agent action logged with actor, action, target, and approval status.

## Audit Principle
Every write (create/update/delete) on goals, visions, and scorecards is logged. v1: Supabase query logs suffice. Later: dedicated `audit_logs` table with actor, action, target_type, target_id, created_at.

## Data Integrity
- Score range enforced by DB check constraint (0–10)
- Unique constraints prevent duplicate scorecard entries
- No cascade deletes — goals archive, never hard-delete in v1