# eco-apps — Data Model

## Table: goals
| Field | Type | Notes |
|------|------|-------|
| id | uuid PK | gen_random_uuid() |
| user_id | uuid | nullable (owner-scoping later) |
| title | text | not null |
| category | text | health / soft_skill / education / career |
| horizon | text | short_term / long_term |
| priority | int | 1–5, default 3 (weighting for score) |
| target_date | date | nullable |
| status | text | active / achieved / archived; default active |
| ai_category_suggestion | text | AI-suggested category |
| ai_category_source | text | model source |
| ai_category_confidence | numeric | 0–1 |
| ai_category_review_status | text | default 'unreviewed' |
| created_at | timestamptz | default now() |

## Table: activities
| Field | Type | Notes |
|------|------|-------|
| id | uuid PK | |
| user_id | uuid | nullable |
| goal_id | uuid | FK → goals.id |
| description | text | not null |
| activity_date | date | not null |
| duration_minutes | int | nullable |
| created_at | timestamptz | default now() |

## Table: weekly_scorecards
| Field | Type | Notes |
|------|------|-------|
| id | uuid PK | |
| user_id | uuid | nullable |
| goal_id | uuid | FK → goals.id |
| week_start | date | Monday of the week |
| rating | int | 0–100, user-entered |
| notes | text | nullable |
| ai_summary | text | AI-generated weekly note |
| ai_summary_source | text | model source |
| ai_summary_confidence | numeric | 0–1 |
| ai_summary_review_status | text | default 'unreviewed' |
| created_at | timestamptz | default now() |

## Table: audit_logs
| Field | Type | Notes |
|------|------|-------|
| id | uuid PK | |
| user_id | uuid | nullable |
| action | text | create / update / delete |
| entity | text | goal / activity / scorecard |
| entity_id | uuid | |
| details | jsonb | nullable |
| created_at | timestamptz | default now() |

## Relationships
- goals 1:N activities (goal_id)
- goals 1:N weekly_scorecards (goal_id)
- activities belong to exactly one goal
- One scorecard row per goal per week (unique constraint on goal_id + week_start)

## RLS Notes
- v1: permissive read/write policies (demo-first, no login)
- Lock-down sprint: replace with `auth.uid() = user_id` policies
- All tables have nullable user_id for future owner-scoping