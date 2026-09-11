# eco-apps — Security

## Secret Handling
- Supabase URL + anon key: public-safe, exposed to client
- Supabase service role key: server-only, never imported in client components
- Any AI provider keys: server-only environment variables
- `.env.local` for local dev; Vercel environment variables for production
- No secrets committed to the repo

## Permission Model
- **v1 (demo-first):** all tables have permissive RLS — anonymous reads and writes work so the app renders without login
- **Lock-down sprint:** replace permissive policies with `auth.uid() = user_id` — each user sees only their own goals, activities, and scorecards
- Agent (when added) inherits the calling user's permissions — cannot exceed what the user can do

## Approved-Tools Rule
- Agent may only call explicitly named tools (see Agentic Layer doc)
- No raw SQL execution, no arbitrary function calls
- Each tool has a defined input shape and write target

## Audit Principle
- Every create/update/delete on goals, activities, and scorecards writes to `audit_logs`
- Every agent action writes to `audit_logs` with action + entity + details
- Audit logs are append-only — no update or delete path

## Honesty Note
If per-user RLS and auth integration proves complex, stop and get a human developer to verify the policies before deploying with real user data.