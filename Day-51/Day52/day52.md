# Day 52 — System Design
## Capstone Project — Day 2 of 10

**Challenge:** ABTalks 60-Day Claude AI Challenge
**Task:** Transform the Day 1 plan into a complete technical blueprint
**Deliverable type:** GitHub commit URL

---

## What I Did Today

Set up the dedicated GitHub repository for the actual product (`gd-prep-coach`, separate from this challenge-log repo) and produced the complete technical design for GD Prep Coach: architecture, database schema, API contract, UI wireframes, and project structure — all before writing a single line of code.

## Repository Setup

- Created `gd-prep-coach` repo on GitHub (public)
- Cloned locally, set up `/client`, `/server`, `/docs` folder structure
- Hit a couple of real beginner Git/terminal issues (folders created one level up by mistake) and fixed them by carefully reading `dir` output and moving files with `move`/`rmdir` — good practical Git practice

## Tech Stack Finalized

React (Vite) + Node.js/Express + MongoDB Atlas + JWT auth + Anthropic Claude API + Web Speech API, deployed on Vercel (frontend) + Render (backend) — 100% free tier, matching the PRD.

## Deliverables Generated

1. `ARCHITECTURE.md` — component diagram, data flow, request lifecycle, AI interaction (Mermaid diagrams)
2. `SCHEMA.md` — full MongoDB collection design (users, topics, attempts) validated against every PRD user story
3. `API.md` — complete endpoint contract for all 10 v1.0 routes, with validation and error cases
4. `UI-WIREFRAMES.md` — user flow diagram, screen list, navigation, low-fi wireframes for every screen
5. `PROJECT-STRUCTURE.md` — full folder layout for client/server, mapped to which Blueprint day touches which files

All committed to [`gd-prep-coach/docs`](https://github.com/ramyanagesh29/gd-prep-coach/tree/main/docs).

## Day 3 Readiness Check

Confirmed: no scope creep, timeline still realistic, Day 3 (GD Topics data model + browsing UI) can begin implementation immediately with zero re-planning.

## Key Learnings

- **Design before code saves real time.** Having the exact schema, API contract, and file structure locked down means tomorrow is pure execution, not decision-making.
- **Real terminal mistakes are part of the process.** Misplaced folders and path confusion are normal — reading command output carefully (`dir`, `git status`) is the actual debugging skill, not avoiding mistakes entirely.
- **Separating the challenge-log repo from the product repo** keeps the actual deployable project clean and resume-ready on its own.

---
**#60DayClaudeChallenge**
