# eco-apps — Product Requirements

## Problem
Goal progress across health, soft skills, and education is hard to track consistently. People pay expensive coaches for accountability that a structured self-assessment tool can provide.

## Target User
The builder and their students — motivated individuals working toward personal growth goals who want a weekly accountability scorecard without paying for a human coach.

## Core Objects
- **Goal** — a specific target with a category (health, soft skill, education, career) and horizon (short-term / long-term)
- **Activity** — a logged action taken toward a goal on a given date
- **Weekly Scorecard** — per-goal progress rating for a given week, plus an overall weekly score

## MVP (v1) Checklist
- [ ] Create, edit, delete goals across 4 categories
- [ ] Log activities against goals
- [ ] Generate a weekly scorecard: rate each active goal 0–100 for the week
- [ ] Auto-compute overall weekly score from goal ratings
- [ ] View current week scorecard and past weeks' scores
- [ ] Trend view showing weekly score over time
- [ ] Works without login (seeded demo data renders immediately)

## Non-Goals (v1)
- No human-in-the-loop checking or mentor approval
- No social/sharing features
- No notifications or reminders
- No payment/subscription system
- No multi-tenant SaaS — personal tool for builder + students

## Success Criteria
A user opens the app, creates a health goal ("Run 3x per week"), logs an activity ("Ran 5km Monday"), opens the weekly scorecard, rates that goal 80/100, and sees the overall weekly score update to reflect it — all without logging in. The scorecard persists to the database and survives a refresh.