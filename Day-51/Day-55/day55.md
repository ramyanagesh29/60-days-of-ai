# Day 55 — Core Feature Development (AI Analysis Engine)
## Capstone Project — Day 5 of 10

**Challenge:** ABTalks 60-Day Claude AI Challenge
**Task:** Build the AI-powered response analysis engine
**Deliverable type:** GitHub commit URL

---

## What I Built Today

Implemented the core AI feature of GD Prep Coach: submitting a Group Discussion response and getting back a real, structured score and feedback — the entire reason this app exists.

**Key decision:** Switched the AI provider from Anthropic Claude (originally planned) to **Google Gemini API**, since Gemini has a genuine free tier with no credit card required, keeping the whole capstone buildable at zero cost.

## Features Implemented

- `Attempt` model to store responses, scores, and structured feedback
- AI analysis service (`analyzeResponse.js`) — builds an evaluation prompt, calls Gemini, defensively parses the JSON response
- `POST /api/attempts` — saves the response **before** calling AI, so nothing is lost even if analysis fails
- `GET /api/attempts/history` — returns a user's past attempts
- Practice page with **text and voice input** (Web Speech API)
- Results page showing score + full feedback breakdown

## Real Debugging Moments

- Hit a `404` error because `gemini-2.0-flash` had been deprecated — fixed by switching to `gemini-3.6-flash`, per Google's own error message.
- Verified the "save-before-analyze" design actually works: two early test attempts show `score: null` in the database from before the fix — proving responses aren't lost even when AI analysis fails.

## Verified Working

- Off-topic response → correctly scored low (15/100) with accurate reasoning ✅
- On-topic but imperfect response → correctly scored higher (40/100) with different, specific feedback ✅
- History endpoint returns correctly scoped, ordered data ✅

## Key Learnings

- **Free-tier AI is genuinely viable for a capstone like this.** Gemini's free tier didn't compromise quality — the feedback was specific and differentiated, not generic.
- **Save-then-analyze is a resilience pattern worth knowing.** Designing so a failure in step 2 (AI call) doesn't destroy step 1's work (saved response) is a real production pattern, not just theory.
- **Deprecation happens — read the error message.** Google's 404 error literally told me the exact fix; the skill was reading it carefully instead of panicking.

---
**#60DayClaudeChallenge**
