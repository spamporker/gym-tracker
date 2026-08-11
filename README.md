# IronLog

A private, mobile-first workout & weigh-in tracker for you and Luke (and anyone else you add to the circle later). Built on plain HTML/JS + Supabase — no build step, easy to edit.

## What's in this folder

- `index.html` — the whole app (UI + logic)
- `config.js` — your Supabase URL + anon key
- `schema.sql` — run once in Supabase SQL Editor to create all tables, security rules, and the exercise library
- `seed_program.sql` — run once **per person** after they sign up, to load your 12-week program template

## First-time setup

1. **Run the schema.** In your Supabase project, open the SQL Editor, paste in `schema.sql`, and run it.
2. **Deploy the app** (see below), then open it on your phone and sign up (you first, then Luke). Signing up automatically creates a profile and adds that person to the shared "circle."
3. **Seed your program.** In Supabase, go to Table Editor → `profiles` to find your `id`. Open `seed_program.sql`, replace `PASTE_USER_ID_HERE` with your id, and run it. Do the same for Luke with his id. This loads Workout A / Workout B for Weeks 1-4 exactly as they were in your spreadsheet.
4. Open the app, log a check-in and a session, and you're live.

## Deploying to GitHub Pages

1. Create a new repo (e.g. `ironlog`) on your new GitHub account.
2. Add `index.html` and `config.js` to the repo root, commit, push.
3. In the repo, go to **Settings → Pages**, set source to the `main` branch, root folder.
4. GitHub gives you a URL like `https://yourusername.github.io/ironlog/` — that's what you and Luke bookmark on your phones (Add to Home Screen makes it feel like an app).

## How it works day to day

- **Today tab** — log this morning's weight/protein/carbs/water/creatine, and log today's workout (pick Workout A or B, fill in reps/weight per set). If you've logged that exercise before, the field shows your last numbers as a placeholder so you can see progressive overload at a glance.
- **History tab** — a scrolling log of your last 30 sessions and check-ins.
- **Circle tab** — a high-level view of everyone in your circle: latest weight, 7-day trend, and sessions this week. Nobody can see anyone else's individual sets or exercises — just the summary.

## Extending later

- **Add someone new** (like a son-in-law): they just sign up in the app — they're automatically added to the circle. No SQL needed.
- **Weeks 5-8 / 9-12**: once you're ready, I can add those as new `program_phases` rows with their own workouts, following the same pattern as `seed_program.sql`. The app automatically picks whichever phase's date range includes today.
- **Design tweaks**: colors and fonts are all CSS variables at the top of `index.html` — easy to retheme.

## A note on the anon key

The key in `config.js` is Supabase's public "anon" key — it's meant to be visible in client-side code. It can't do anything your Row Level Security policies (in `schema.sql`) don't explicitly allow, which is why locking those down correctly matters more than hiding this key.
