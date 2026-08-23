# Day 53 — Project Setup & Foundation
## Capstone Project — Day 3 of 10

**Challenge:** ABTalks 60-Day Claude AI Challenge
**Task:** Build the project's foundation — environment, folder structure, DB connection, auth scaffold, routing
**Deliverable type:** GitHub commit URL

---

## What I Built Today

Set up the complete technical foundation for GD Prep Coach — no features yet, just a fully working skeleton ready for real feature development tomorrow.

**Backend:** Express server with MongoDB Atlas connection, health-check route, User model, and JWT auth middleware scaffold.

**Frontend:** React (Vite) app with React Router wired up across all 7 planned screens, a working NavBar, and a pre-configured Axios client with automatic JWT attachment.

**Database:** Discovered MongoDB Atlas free tier only allows one cluster per project — created a dedicated new Atlas project just for this capstone to get a clean, separate free cluster.

## Biggest Real-World Debugging Moment

Hit a genuine "MongoDB connection error: could not connect to any servers" — turned out to be an IP whitelist issue. Fixed it via Network Access → Allow Access from Anywhere. Small thing, but it's the kind of real deployment friction that's actually useful to hit and solve myself.

## Verified Working

- Backend running on `localhost:5000`, MongoDB connected ✅
- Frontend running on `localhost:5173`, all routes navigable ✅
- `/api/health` returns correct JSON ✅

## Deliverables Generated

1. `SETUP.md` — full install/setup guide
2. `ENVIRONMENT.md` — all env vars and MongoDB Atlas config documented
3. `PROJECT-STRUCTURE.md` — updated with ✅/⏳ status per file
4. `DAY3-SUMMARY.md` — full day recap

All committed to [`gd-prep-coach/docs`](https://github.com/ramyanagesh29/gd-prep-coach/tree/main/docs).

## Key Learnings

- **Free-tier constraints are real constraints.** The "one cluster per project" limit wasn't in any tutorial I'd seen — solving it (new Atlas project) was a genuine problem-solving moment, not just following steps.
- **Scaffolding before features prevents rework.** Having routing, DB connection, and auth middleware working *before* writing any real feature logic means tomorrow is pure feature-building, no plumbing.
- **Reading terminal/error output carefully is the actual skill.** Every hiccup today (wrong folder, IP whitelist, lost password) was solved by reading the exact error message, not guessing.

---
**#60DayClaudeChallenge**
