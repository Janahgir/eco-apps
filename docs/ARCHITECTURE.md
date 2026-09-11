# eco-apps — Architecture

## Stack
- Next.js 14 (App Router) + TypeScript
- Supabase (Postgres + RLS)
- Vercel deployment
- Tailwind CSS for UI

## Build Now vs Later
**Now:** goals CRUD, activity logging, weekly scorecard creation + scoring, trend dashboard.
**Later:** AI weekly summaries, goal category suggestions, streaks/badges, auth + per-user isolation.

## Key User Action Flow (Weekly Scorecard)
1. User opens app → lands on dashboard showing current week
2. User creates a goal (or selects existing seeded goal)
3. User logs an activity against that goal for the week
4. User opens weekly scorecard → rates each active goal 0–100
5. System computes overall weekly score (average of goal ratings, weighted by goal priority)
6. Scorecard persists; dashboard updates with new score and trend line

## Responsive Nav Shell
Left sidebar on desktop (Goals, Activities, Scorecard, Trends) collapsing to hamburger on mobile. Current section highlighted. Keyboard accessible.

## Layer Plan
1. **Data layer** (`lib/data/`) — all DB reads/writes: goals, activities, scorecards
2. **App logic** (`lib/actions/`) — server actions for create/update/delete, score computation
3. **Smart features** (`lib/ai/`) — weekly summary generation (later)
4. **UI** (`app/` + `components/`) — screens and components calling data layer only

## Why Core Runs Without AI
Scoring is a deterministic weighted average of user-entered ratings. Activity logging and goal management are pure CRUD. The AI layer only adds optional summaries on top.

## Repo Structure
```
eco-apps/
├── app/
│   ├── page.tsx              (dashboard)
│   ├── goals/page.tsx
│   ├── activities/page.tsx
│   ├── scorecard/page.tsx
│   ├── trends/page.tsx
│   └── layout.tsx
├── components/
│   ├── GoalForm.tsx
│   ├── ActivityForm.tsx
│   ├── ScorecardForm.tsx
│   ├── TrendChart.tsx
│   └── Sidebar.tsx
├── lib/
│   ├── data/                 (goals.ts, activities.ts, scorecards.ts)
│   ├── actions/              (goal-actions.ts, activity-actions.ts, scorecard-actions.ts)
│   ├── ai/                   (summary.ts — later)
│   └── scoring.ts            (weekly score computation)
├── tests/
│   ├── scoring.test.ts
│   └── scorecard.test.ts
└── supabase/migrations/
```

## Module Map
| Module | Responsibility | Data Owned | Build Order |
|--------|---------------|------------|-------------|
| goals | Goal CRUD + categories | goals table | 1st |
| activities | Activity logging against goals | activities table | 2nd |
| scorecard | Weekly scorecard creation + scoring | weekly_scorecards table | 3rd |
| trends | Score visualization over time | reads scorecards | 4th |
| ai-summary | Auto-generate weekly summary text | writes to scorecards.summary | 5th |
| auth | Login + per-user isolation | RLS policies | 6th |