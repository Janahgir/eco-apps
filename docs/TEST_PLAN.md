# eco-apps — Test Plan

## V1 Success Scenario (Manual)
1. Open app in browser (no login) → dashboard renders with seeded goals
2. Click "Goals" in sidebar → see seeded goals (health, soft skill, education)
3. Click "New Goal" → enter "Run 3x per week", category health, horizon short-term, priority 4 → save
4. New goal appears in list, persists after refresh
5. Click "Activities" → select "Run 3x per week" → enter "Ran 5km Monday", date today → save
6. Activity appears in list, linked to goal
7. Click "Scorecard" → current week shown → rate "Run 3x per week" as 80 → save
8. Overall weekly score updates (weighted average including other rated goals)
9. Return to dashboard → current week score visible
10. Refresh page → all data persists

## Empty States
- **No goals:** Goals page shows "No goals yet. Create your first goal to start tracking." with a visible "New Goal" button
- **No activities:** Activities page shows "No activities logged yet. Log an activity to track your progress."
- **No scorecard:** Scorecard page shows "No scorecard for this week yet. Rate your goals to create one." with active goals listed for quick rating
- **No trend data:** Trends page shows "Not enough data yet. Complete at least 2 weekly scorecards to see trends."

## Error States
- **DB unreachable:** Show "Something went wrong loading goals. Please try again." with retry button — not a blank screen
- **Invalid form input:** Submit goal without title → inline validation error "Title is required"
- **Duplicate scorecard:** Rate same goal same week twice → show "You already rated this goal this week. Edit the existing rating instead."
- **Delete with linked activities:** Deleting a goal with activities → confirm dialog "This goal has 3 activities. Delete anyway?" → cascade or block

## Loading States
- Goals list: skeleton cards while fetching
- Scorecard form: spinner while loading existing ratings
- Dashboard: loading state for score before populated

## Permission Tests (Sprint 5)
- Log in as User A → create a goal → log out → log in as User B → cannot see User A's goal
- Unauthenticated user → redirected to login (or demo mode shows only seed data)