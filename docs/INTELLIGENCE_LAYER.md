# eco-apps — Intelligence Layer

## Messy Inputs
- Free-text goal titles ("get better at talking to people")
- Free-text activity descriptions ("ran", "did some reading")
- Weekly notes (varied length, informal)

## Auto-Structure Schema (Goal)
```json
{
  "title": "get better at talking to people",
  "structured": {
    "category": "soft_skill",
    "confidence": 0.88,
    "suggested_title": "Improve communication confidence in group settings"
  }
}
```

## Events to Track
- goal_created, goal_updated, goal_achieved
- activity_logged
- scorecard_rated, scorecard_completed
- weekly_score_computed

## Scoring Rules (v1, rule-based)
- Per-goal rating: user enters 0–100 per goal each week
- Overall weekly score = weighted average of goal ratings, weight = goal.priority (1–5)
- If no rating entered for a goal this week → excluded from average (not zero)
- Weekly score rounded to nearest integer
- Streak: consecutive weeks with score ≥ 70

## What Gets Ranked
- Goals by recent rating trend (improving/declining/steady)
- Weeks by overall score (best weeks, worst weeks)

## v1 vs Later
- **v1:** deterministic scoring (weighted average), manual rating entry
- **Later:** AI weekly summary per scorecard, AI category suggestions for goals, AI-flagged declining goals, smart activity tagging