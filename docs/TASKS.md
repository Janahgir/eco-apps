# eco-apps — Tasks

## Sprint 1: Foundation + Goals CRUD
**Goal:** DB schema live, goals can be created/edited/deleted, app renders with seed data — no login.
- [ ] Create Supabase migration (all tables + RLS + seed data)
- [ ] Build `lib/data/goals.ts` (CRUD queries)
- [ ] Build `lib/actions/goal-actions.ts` (server actions)
- [ ] Build goals page: list + create form + edit + delete
- [ ] Build responsive sidebar shell (desktop sidebar, mobile hamburger)
- [ ] Build dashboard page showing goals summary
- [ ] Loading, empty, and error states for goals page
**DoD:** User can create a goal, see it in the list, edit it, delete it — persists to DB, survives refresh. Seeded goals render on first load.

## Sprint 2: Activities + Weekly Scorecard (v1 FUNCTIONAL MILESTONE)
**Goal:** The core engine works — user logs activities and rates goals weekly.
- [ ] Build `lib/data/activities.ts` + actions
- [ ] Build activities page: log activity against a goal with date + description
- [ ] Build `lib/scoring.ts` (weighted average computation)
- [ ] Build `lib/data/scorecards.ts` + actions
- [ ] Build scorecard page: select week, rate each active goal 0–100, see overall score
- [ ] Unique constraint: one rating per goal per week
- [ ] Loading, empty, partial, error states for both pages
**DoD:** User logs an activity, opens the weekly scorecard, rates a goal, and sees the overall weekly score update. Full success scenario works end-to-end.

## Sprint 3: Trends + Dashboard Polish
**Goal:** User can see progress over time.
- [ ] Build trends page: weekly score line chart over past 8 weeks
- [ ] Build per-goal trend cards (rating over time)
- [ ] Dashboard: current week score, goal count by category, recent activities
- [ ] Empty state: "No scorecards yet — create your first weekly scorecard"
- [ ] Streak indicator (consecutive weeks ≥ 70)
**DoD:** Dashboard shows current week score + trend chart with at least 2 weeks of seeded data.

## Sprint 4: AI Summaries
**Goal:** Smart features on top of the working core.
- [ ] Build `lib/ai/summary.ts` — generate weekly summary from activities + ratings
- [ ] Show AI summary on scorecard with review_status badge
- [ ] Goal category suggestion on goal creation form
- [ ] AI fields: value + source + confidence + review_status stored correctly
**DoD:** Creating a scorecard with activities generates an AI summary visible on the scorecard page.

## Sprint 5: Lock It Down
**Goal:** Auth + per-user data isolation.
- [ ] Add Supabase Auth (sign up / log in)
- [ ] Replace permissive RLS with `auth.uid() = user_id` policies
- [ ] Set user_id on all creates from session
- [ ] Redirect unauthenticated users to login (keep demo mode toggle for builder)
- [ ] Test: user A cannot see user B's goals
**DoD:** Two logged-in users see only their own data. Logout clears session. No cross-user data leak.

---

## Text Gantt
```
Task                    S1  S2  S3  S4  S5
Goals CRUD              ██
Activities logging         ██
Weekly scorecard           ██
Scoring engine             ██
Trends dashboard               ██
Dashboard polish                ██
AI summaries                       ██
Goal suggestions                   ██
Auth + RLS                             ██
Per-user isolation                     ██
```

**v1 functional milestone = end of Sprint 2.**