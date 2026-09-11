# eco-apps — Agentic Layer

## Risk Levels

### Low (auto-execute)
- **Generate weekly summary** — AI writes a 2–3 sentence summary of the week's activities + ratings → stored in `weekly_scorecards.ai_summary` with `review_status = 'unreviewed'`
- **Suggest goal category** — AI proposes category for new goals → stored in `goals.ai_category_suggestion`
- **Tag activity** — AI normalizes activity description (later)

### Medium (draft, light approval)
- **Draft goal updates** — AI suggests revised target dates or priority based on trend → user approves before save

### High (always approval)
- **Send weekly recap email** — (later) requires explicit confirmation

### Critical (human-only)
- **Delete goal** — only the user can delete; agent never deletes
- **Archive goal** — only the user can archive

## Named Tools
- `generate_weekly_summary(goal_id, week_start)` → writes ai_summary fields
- `suggest_goal_category(title)` → writes ai_category_suggestion fields
- `draft_goal_update(goal_id)` → returns suggestion, no write

No raw execution tools. Agent uses approved named tools only.

## Audit Log Fields
Every agent action logs: action, entity, entity_id, details (jsonb), user_id, created_at.

## v1 vs Later
- **v1:** none of these run automatically — scoring is deterministic and user-driven
- **Later:** weekly summary generation on scorecard completion, category suggestions on goal creation