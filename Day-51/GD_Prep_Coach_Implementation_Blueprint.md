# GD Prep Coach — Implementation Blueprint (Days 2–10)

**Project:** GD Prep Coach — AI-powered Group Discussion practice & analysis platform
**Capstone:** ABTalks 60-Day Claude AI Challenge — 10-Day Capstone
**Builder background:** Comfortable with REST APIs, CRUD, MongoDB, Node.js, Express
**Deployment constraint:** Free-tier hosting only, no paid services
**How to use this document:** Each day below is self-contained. Start each day's AI conversation by pasting that day's section (plus the PRD if needed). It contains enough context that a fresh AI conversation can continue building without re-planning architecture.

---

## Locked Decisions (apply to every day — do not re-decide)

- **Architecture:** 3-tier — React frontend, Node.js/Express backend (REST API), MongoDB database.
- **Auth:** JWT-based, stored in localStorage on frontend, verified via Express middleware.
- **AI:** Anthropic Claude API called from the **backend only** (never expose API key in frontend). Single well-scoped call per analysis action.
- **Voice input:** Browser Web Speech API (`SpeechRecognition`) — converts speech to text client-side, no audio files stored or sent to backend.
- **Hosting (free-tier):** Frontend on Vercel (or Netlify), Backend on Render (free web service), Database on MongoDB Atlas (free M0 cluster).
- **Repo:** Single GitHub repo, two folders: `/client` (React) and `/server` (Express).
- **Out of scope reminders:** No push notifications, no audio/tone ML analysis, no live multi-user rooms, no payments. If any day's work drifts toward these, stop and flag it instead of building it.

---

## Day 2 — Tech Stack Finalization, Project Setup & Auth Backend

### 🎯 Objective
Finalize exact tool versions, scaffold the repo (client + server), set up MongoDB Atlas, and build a working signup/login API with JWT auth.

### 📖 What I'll learn
Project scaffolding conventions, environment variable management, MongoDB Atlas setup, password hashing, JWT issuing/verification middleware.

### 🛠 Features to build
- Express server skeleton with health-check route
- MongoDB Atlas connection
- `User` model (name, email, password hash)
- `/api/auth/signup` and `/api/auth/login` routes
- JWT auth middleware (`protect` function) for future protected routes

### 📝 Step-by-step implementation plan
1. Create GitHub repo `gd-prep-coach` with `/client` and `/server` folders.
2. In `/server`: `npm init -y`, install `express mongoose bcryptjs jsonwebtoken cors dotenv`.
3. Create `.env` with `MONGO_URI`, `JWT_SECRET`, `PORT=5000` — add `.env` to `.gitignore`.
4. Guided manual step: create a free MongoDB Atlas cluster (M0), create a DB user, whitelist all IPs (0.0.0.0/0) for now, copy connection string into `.env`.
5. Build `server.js`: Express app, `cors()`, `express.json()`, connect to Mongo via Mongoose, `app.listen`.
6. Create `models/User.js` (fields: name, email unique, passwordHash, createdAt).
7. Create `routes/auth.js`: signup (hash password with bcrypt, save user, return JWT), login (compare hash, return JWT).
8. Create `middleware/auth.js`: verifies `Authorization: Bearer <token>` header, attaches `req.userId`.
9. In `/client`: `npx create-vite@latest client -- --template react`, install `axios react-router-dom`.
10. Build minimal Signup and Login pages calling the API, storing JWT in localStorage.
11. Test full flow locally: signup → login → token stored.

### 📂 Files and folders to create or modify
```
/server
  server.js
  .env
  models/User.js
  routes/auth.js
  middleware/auth.js
/client
  src/pages/Signup.jsx
  src/pages/Login.jsx
  src/api/axios.js
```

### 🔗 APIs, libraries, services, or tools to integrate
- MongoDB Atlas (free M0 cluster)
- bcryptjs, jsonwebtoken, mongoose, cors, dotenv (npm)
- React Router for page navigation

### 🧪 Testing tasks
- Signup with a new email → 201 + token returned.
- Signup with duplicate email → clear 400 error, no crash.
- Login with wrong password → 401, no crash.
- Protected test route rejects requests with no/invalid token.

### 🐞 Common issues and debugging tips
- Mongoose connection hanging: check Atlas IP whitelist and that the password in the connection string has special characters URL-encoded.
- CORS errors from React dev server: confirm `cors()` is applied before routes.
- JWT "invalid signature": make sure `JWT_SECRET` is identical everywhere and `.env` is actually loaded (`require('dotenv').config()` at the very top of `server.js`).

### ✅ End-of-day checklist
- [ ] MongoDB Atlas cluster created and connected from server.js
- [ ] Signup and Login endpoints working, tested with Postman/Thunder Client
- [ ] JWT issued and verifiable by middleware
- [ ] React app scaffolded with working Signup/Login forms hitting the real API
- [ ] Code pushed to GitHub

### 📸 Expected project state and screenshots to capture
- Screenshot: successful signup response in Postman/Thunder Client
- Screenshot: React signup/login forms in browser
- Screenshot: MongoDB Atlas showing the new `users` collection with a test user

### ➡️ Handoff notes for Day 3
Auth backend and basic frontend auth pages exist and work end to end. Day 3 builds the GD Topic model/API and the topic browsing UI on top of this authenticated foundation. JWT middleware (`middleware/auth.js`) is ready to protect new routes.

---

## Day 3 — GD Topics: Data Model, Seed Content & Browsing UI

### 🎯 Objective
Build the GD topic library (curated content) with category filtering, backed by a real DB collection, and a frontend page to browse/select topics.

### 📖 What I'll learn
Schema design for content libraries, seeding a database, building filterable list UIs in React.

### 🛠 Features to build
- `Topic` model (title, category, description)
- Seed script with ~20-30 curated GD topics across 3-4 categories (current affairs, abstract, case-study, social issues)
- `/api/topics` (list, filter by category) — protected route
- Frontend Topics page: category filter + topic cards, "Start Practice" button per topic

### 📝 Step-by-step implementation plan
1. Create `models/Topic.js` (title, category, description, createdAt).
2. Write `seed/seedTopics.js` with curated topics (write these yourself, grouped by category — this is content, not code logic).
3. Run seed script once to populate the Atlas collection.
4. Create `routes/topics.js`: `GET /api/topics` (optional `?category=` query param), protected by auth middleware.
5. In client, create `TopicsPage.jsx`: fetch topics on load, category filter dropdown/tabs, topic cards.
6. Clicking a topic card navigates to `/practice/:topicId` (route built out Day 4).
7. Add basic navigation bar (Dashboard | Topics | History | Logout).

### 📂 Files and folders to create or modify
```
/server
  models/Topic.js
  routes/topics.js
  seed/seedTopics.js
/client
  src/pages/TopicsPage.jsx
  src/components/TopicCard.jsx
  src/components/NavBar.jsx
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new — reuse Mongoose, Express, Axios from Day 2.

### 🧪 Testing tasks
- Seed script runs without duplicate key errors (make it idempotent — check if topics exist before inserting).
- `/api/topics` returns full list; `/api/topics?category=Abstract` returns filtered subset only.
- Frontend topic list renders correctly and category filter updates the visible cards.
- Route is rejected (401) if accessed without a valid JWT.

### 🐞 Common issues and debugging tips
- Re-running seed script duplicates data: add a check/clear step, or use `insertMany` with a guard on collection count.
- Frontend shows blank list: check the JWT is actually being sent in the `Authorization` header via an Axios interceptor.
- Category filter not matching: ensure category strings are consistent (exact casing) between seed data and frontend filter values.

### ✅ End-of-day checklist
- [ ] Topic model created, 20-30 topics seeded across categories
- [ ] `/api/topics` working with category filtering, protected by auth
- [ ] Topics page in React shows cards with working category filter
- [ ] Navigation bar in place across authenticated pages

### 📸 Expected project state and screenshots to capture
- Screenshot: Topics page showing category filter and topic cards
- Screenshot: MongoDB Atlas `topics` collection populated

### ➡️ Handoff notes for Day 4
Topics exist in the DB and are browsable. Day 4 builds the actual practice session flow: selecting a topic, responding via text or voice, and submitting a response for analysis (analysis itself is Day 5).

---

## Day 4 — Practice Session Flow: Text + Voice Input

### 🎯 Objective
Build the practice session screen where a user responds to a topic by typing or speaking, with the response captured as text and ready to submit.

### 📖 What I'll learn
Web Speech API integration, building controlled text inputs in React, structuring a "session" data model in the backend ahead of AI integration.

### 🛠 Features to build
- Practice session page: shows selected topic, text area for response, "Speak" button using Web Speech API, "Submit" button
- `Attempt` model (userId, topicId, responseText, inputMethod, createdAt) — score/feedback fields added Day 5
- `POST /api/attempts` to save a raw attempt (without AI analysis yet, to unblock this day's testing)

### 📝 Step-by-step implementation plan
1. Create `models/Attempt.js` with fields: `userId`, `topicId`, `responseText`, `inputMethod` (`"text"` or `"voice"`), `score` (null for now), `feedback` (null for now), `createdAt`.
2. Create `routes/attempts.js`: `POST /api/attempts` saves userId (from JWT), topicId, responseText, inputMethod.
3. In client, build `PracticePage.jsx`:
   - Fetch topic details by `topicId` from route params.
   - Textarea bound to state for typed response.
   - "🎤 Speak" button: use `window.SpeechRecognition || window.webkitSpeechRecognition`, on result append transcribed text into the textarea state.
   - Show a clear "Listening..." indicator while recognition is active.
   - "Submit" button posts to `/api/attempts`, then navigates to a results placeholder page (wired fully Day 5).
4. Handle browsers without SpeechRecognition support: hide/disable the Speak button and show a note that voice works best in Chrome, but text input always works.

### 📂 Files and folders to create or modify
```
/server
  models/Attempt.js
  routes/attempts.js
/client
  src/pages/PracticePage.jsx
  src/hooks/useSpeechRecognition.js
```

### 🔗 APIs, libraries, services, or tools to integrate
- Browser Web Speech API (`SpeechRecognition`) — no npm package needed, built into Chrome.

### 🧪 Testing tasks
- Typing a response and submitting saves an Attempt document correctly in MongoDB.
- Speaking a response transcribes into the textarea accurately (test in Chrome).
- Submitting with empty response is blocked with a friendly inline message.
- Confirm `userId` on saved attempts matches the logged-in user (test with two different accounts).

### 🐞 Common issues and debugging tips
- `SpeechRecognition` undefined: confirm testing in Chrome, not Firefox/Safari (limited support) — this is a known browser constraint, not a bug.
- Recognition stops after a short pause: set `recognition.continuous = true` and restart it if it ends unexpectedly while the user is still speaking.
- Duplicate text on multiple speech results: append only the final transcript segment, not the full accumulated result each time.

### ✅ End-of-day checklist
- [ ] Practice page shows topic + text input + working Speak button (tested in Chrome)
- [ ] Submitting a response saves a real Attempt document in MongoDB with correct userId/topicId
- [ ] Graceful fallback message shown if browser doesn't support voice input

### 📸 Expected project state and screenshots to capture
- Screenshot: Practice page with a topic and filled-in response (typed)
- Screenshot: Practice page mid-voice-capture showing "Listening..." state
- Screenshot: MongoDB `attempts` collection showing a saved raw attempt

### ➡️ Handoff notes for Day 5
Users can submit typed or spoken responses, saved as Attempts with `score`/`feedback` fields still null. Day 5 wires up the actual Claude API call to analyze `responseText` and populate those fields, then displays results to the user.

---

## Day 5 — Claude API Integration: AI Analysis Engine

### 🎯 Objective
Connect the Anthropic Claude API on the backend to analyze each submitted response and return a structured score + feedback, and display results to the user.

### 📖 What I'll learn
Calling the Claude API from a Node backend, prompt design for structured/consistent output, parsing AI responses safely, API key/credit management.

### 🛠 Features to build
- Claude API key setup (guided manual step)
- Backend service that sends the response + topic to Claude with a structured analysis prompt
- Update `Attempt` on submission with `score`, `feedback` (structured: strengths, improvements)
- Results page in frontend showing score + feedback clearly

### 📝 Step-by-step implementation plan
1. **Guided manual step:** create an Anthropic API key at the Anthropic Console, add starting credits (I'll walk you through each screen with confirmation before continuing).
2. Install `@anthropic-ai/sdk` in `/server`; add `ANTHROPIC_API_KEY` to `.env`.
3. Create `services/analyzeResponse.js`: builds a prompt instructing Claude to act as a GD evaluator, given the topic and the user's response, and to return **strict JSON** with fields: `score` (0-100), `clarity`, `structure`, `relevance`, `assertiveness` (short comments each), `overallFeedback` (2-3 sentences), `improvementTips` (array of 2-3 short actionable tips).
4. Parse the JSON response defensively (strip markdown code fences if present, `JSON.parse` in a try/catch, fallback error message if parsing fails).
5. Update `POST /api/attempts` (or add `POST /api/attempts/:id/analyze`) to call this service after saving the raw attempt, then update the Attempt document with the results.
6. Build `ResultsPage.jsx`: displays the score prominently (e.g., a simple progress ring or colored badge), then the breakdown comments and improvement tips.
7. Add a loading state on submit ("Analyzing your response...") since the AI call takes a few seconds.

### 📂 Files and folders to create or modify
```
/server
  services/analyzeResponse.js
  routes/attempts.js (updated)
/client
  src/pages/ResultsPage.jsx
  src/components/ScoreBadge.jsx
```

### 🔗 APIs, libraries, services, or tools to integrate
- Anthropic Claude API (`@anthropic-ai/sdk`), model: use the current recommended general-purpose Claude model at time of building — confirm the exact model string in the Anthropic Console/docs rather than assuming one.

### 🧪 Testing tasks
- Submit a strong, well-structured response → verify score is high and feedback is coherent.
- Submit a weak, one-line response → verify score is low and tips are genuinely useful, not generic.
- Simulate an API failure (temporarily use a wrong key) → confirm the app shows a friendly error, not a crash.
- Confirm no API key is ever visible in frontend network requests (check browser dev tools).

### 🐞 Common issues and debugging tips
- Claude returns JSON wrapped in ```json fences: strip these before `JSON.parse`.
- Inconsistent score formatting: constrain the prompt tightly (explicit instruction: "Respond with ONLY valid JSON, no other text") and validate the shape before saving.
- Slow responses: make sure the frontend shows a spinner/loading text so it doesn't look frozen.
- 401 from Anthropic: check `.env` key is loaded and credits are available on the account.

### ✅ End-of-day checklist
- [ ] Claude API key created and working from backend
- [ ] Analysis service returns consistent structured JSON for varied test inputs
- [ ] Attempt document updated with real score/feedback after submission
- [ ] Results page displays score + feedback clearly with loading state handled

### 📸 Expected project state and screenshots to capture
- Screenshot: Results page showing a real AI-generated score and feedback
- Screenshot: Anthropic Console showing API usage/credits
- Screenshot: MongoDB Attempt document with populated score/feedback fields

### ➡️ Handoff notes for Day 6
The core AI loop (submit → analyze → view results) is fully working end to end. Day 6 builds Practice History (list of past attempts) and the Streak & Goals dashboard on top of this data.

---

## Day 6 — Practice History & Streak/Goals Dashboard

### 🎯 Objective
Let users see their past attempts over time and track a practice streak and weekly goal, with an in-app reminder if behind.

### 📖 What I'll learn
Aggregating and displaying time-series data, simple streak-calculation logic, building a dashboard UI.

### 🛠 Features to build
- `GET /api/attempts/history` — returns the logged-in user's past attempts, newest first
- Streak calculation logic (consecutive days with at least one attempt)
- Simple weekly goal (e.g., stored per user: `weeklyGoal` count, defaults to 3) and progress tracking
- Dashboard page: streak counter, weekly goal progress bar, recent scores list, in-app reminder banner if behind pace

### 📝 Step-by-step implementation plan
1. Add `weeklyGoal` field (default 3) to `User` model; add a simple `PUT /api/users/goal` route to update it.
2. Create `routes/attempts.js` addition: `GET /api/attempts/history` returns all attempts for `req.userId`, sorted by `createdAt` descending.
3. Write a small utility `calculateStreak(attemptDates)`: count consecutive calendar days ending today/yesterday with at least one attempt.
4. Write `calculateWeekProgress(attemptDates, weeklyGoal)`: count attempts since the most recent Monday (or last 7 days), compare to goal.
5. Build `DashboardPage.jsx`: streak number with a simple flame/badge icon, progress bar toward weekly goal, "You're behind — practice today!" banner if progress < expected pace for the day of week, and a compact list of last 5 attempts with scores.
6. Build `HistoryPage.jsx`: full scrollable/paginated list of all past attempts with topic, score, and date; clicking one shows full feedback (reuse `ResultsPage` in a read-only mode, or a simple detail view).

### 📂 Files and folders to create or modify
```
/server
  utils/streak.js
  routes/attempts.js (updated)
  routes/users.js
/client
  src/pages/DashboardPage.jsx
  src/pages/HistoryPage.jsx
  src/components/StreakBadge.jsx
  src/components/GoalProgressBar.jsx
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new — pure logic + existing stack.

### 🧪 Testing tasks
- Create test attempts on multiple different dates (manually adjust `createdAt` in DB for testing) and confirm streak counts correctly, including a broken streak resetting to 0/1 correctly.
- Confirm weekly goal progress resets appropriately at the start of a new week.
- Confirm reminder banner appears/disappears correctly based on progress.
- History page correctly shows all attempts only for the logged-in user (test with two accounts).

### 🐞 Common issues and debugging tips
- Timezone bugs in streak calculation: normalize all dates to a single timezone (or just calendar-date strings) before comparing.
- Off-by-one errors in "consecutive days": test explicitly with attempts on today, yesterday, and a gap 3 days ago.
- Large history lists slow to load: add basic pagination or a reasonable limit (e.g., 20 per page) if needed.

### ✅ End-of-day checklist
- [ ] Streak and weekly goal calculated correctly against test data
- [ ] Dashboard shows streak, goal progress, reminder banner, and recent scores
- [ ] History page lists all past attempts correctly, scoped per user

### 📸 Expected project state and screenshots to capture
- Screenshot: Dashboard with a visible streak and goal progress bar
- Screenshot: Reminder banner state (behind pace)
- Screenshot: History page with multiple past attempts listed

### ➡️ Handoff notes for Day 7
Core product is now feature-complete end to end (auth → topics → practice → AI analysis → history/streak). Day 7 focuses on UI/UX polish and the stretch AI-topic-generation feature if time allows — no new core architecture from here.

---

## Day 7 — UI/UX Polish & Stretch Feature (AI Topic Generator)

### 🎯 Objective
Polish the visual design across all pages for a professional look, and add the "Generate new topic" stretch feature if on schedule.

### 📖 What I'll learn
Applying a consistent design system in React, conditionally shipping stretch scope without risking core stability.

### 🛠 Features to build
- Consistent design system: color palette, typography, spacing, responsive layout across all pages
- Loading/empty/error states polished everywhere (not just AI analysis)
- **Stretch:** `POST /api/topics/generate` — Claude generates a new topic + description on demand, saved to DB and shown immediately

### 📝 Step-by-step implementation plan
1. Define a small design system: pick 2-3 core colors + 1 accent, consistent font, consistent spacing scale (e.g., 8px grid). Apply via a shared CSS file or Tailwind if already comfortable with it, otherwise plain CSS modules.
2. Pass over every page (Login, Signup, Topics, Practice, Results, Dashboard, History) and apply consistent buttons, cards, spacing, and typography.
3. Add empty states: no attempts yet, no topics in a category, etc. — friendly messages, not blank screens.
4. Add error boundaries/toasts for failed API calls across the app (a small reusable `Toast` component).
5. Mobile-check every page at a narrow width and fix any overflow/wrapping issues.
6. **If on schedule:** build `POST /api/topics/generate` (category input → Claude generates a title + short description in strict JSON → saved as a new Topic document → returned to frontend and added to the visible list immediately). Add a "✨ Generate New Topic" button on the Topics page.
7. **If behind schedule:** skip step 6 entirely — note it as a "not shipped in v1.0" item for the pitch deck's future scope, and spend the full day on polish instead. This decision must be made explicitly, not by running out of time silently.

### 📂 Files and folders to create or modify
```
/client
  src/styles/theme.css (or tailwind.config.js)
  src/components/Toast.jsx
  src/components/EmptyState.jsx
/server
  routes/topics.js (updated, if building stretch feature)
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new for polish. Claude API reused for stretch topic generation.

### 🧪 Testing tasks
- Every page checked at mobile width (375px) and desktop width — no overflow, no cut-off text.
- Every empty state (no history, no topics) shows a friendly message, never a blank/broken screen.
- Failed API calls show a visible error message, not a silent failure.
- If built: generated topics are saved correctly and appear without a page refresh.

### 🐞 Common issues and debugging tips
- Inconsistent spacing after adding new components: recheck against your spacing scale, don't eyeball it per page.
- Mobile nav overflow: consider a simple hamburger menu if the navbar doesn't fit on small screens.
- Stretch feature scope creep: if the topic generator starts needing "regenerate," "save favorites," etc., stop — that's beyond v1.0.

### ✅ End-of-day checklist
- [ ] All core pages visually consistent and mobile-responsive
- [ ] Empty and error states handled everywhere
- [ ] Decision made and recorded: stretch AI-topic-generator shipped or explicitly deferred

### 📸 Expected project state and screenshots to capture
- Screenshot: Topics page (polished) on desktop and mobile
- Screenshot: Dashboard (polished) on desktop and mobile
- Screenshot (if built): AI-generated topic appearing after clicking "Generate"

### ➡️ Handoff notes for Day 8
Visual design is finalized and consistent. Day 8 is dedicated to structured testing (functional + edge cases) and bug fixing before deployment — no new features introduced.

---

## Day 8 — Structured Testing & Bug Fixing

### 🎯 Objective
Systematically test the entire application end to end, log and fix bugs, and harden the app before deployment.

### 📖 What I'll learn
Manual test-case design, systematic bug triage, defensive coding for edge cases (a skill directly relevant to technical interviews).

### 🛠 Features to build
- No new features — this day is testing and fixing only
- A simple `TESTING.md` checklist/log documenting what was tested and what was fixed (useful evidence for interviews)

### 📝 Step-by-step implementation plan
1. Write a test checklist covering every flow: signup/login (valid + invalid), topic browsing/filtering, practice submission (text + voice, empty input, very long input), AI analysis (normal + edge-case responses), history/streak accuracy, goal editing.
2. Go through the checklist manually, on both desktop and mobile browser, logging any bug found (short description + steps to reproduce) in `TESTING.md`.
3. Fix bugs in priority order: broken core flows first (auth, submission, analysis), then edge cases, then cosmetic issues.
4. Specifically stress-test the AI analysis service: extremely short responses, responses with special characters/emoji, responses in a mix of English and another language — confirm no crashes, only graceful handling.
5. Re-test authentication edge cases: expired/invalid token behavior, accessing another user's data via the API directly (should always be blocked using `req.userId` scoping, never a client-supplied ID).
6. Verify environment variables and secrets are not committed to GitHub (`.env` in `.gitignore`, check `git log` if unsure).

### 📂 Files and folders to create or modify
```
/TESTING.md
(bug fixes across existing /server and /client files as needed)
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new.

### 🧪 Testing tasks
- Full checklist executed and logged (this day's entire task IS testing).
- Confirm no user can view/edit another user's attempts or profile via direct API calls.
- Confirm `.env`/secrets are never in the Git history.

### 🐞 Common issues and debugging tips
- Data leaking between users: always filter DB queries by `req.userId` from the verified JWT, never trust a userId from the request body/params.
- Silent AI failures: make sure every Claude API call path has a try/catch with a user-visible fallback message.
- Accidentally committed `.env`: if found in history, rotate the secrets (new JWT secret, new Mongo password, new API key) rather than just deleting the file going forward.

### ✅ End-of-day checklist
- [ ] Full test checklist completed and logged in `TESTING.md`
- [ ] All critical/core-flow bugs fixed
- [ ] Security check done: no cross-user data leaks, no committed secrets

### 📸 Expected project state and screenshots to capture
- Screenshot: `TESTING.md` checklist with items marked complete
- Screenshot: any before/after of a notable bug fixed (optional but great for a LinkedIn post)

### ➡️ Handoff notes for Day 9
App is functionally solid and tested. Day 9 is dedicated entirely to deployment: getting the frontend, backend, and database live on free-tier hosting with a public URL.

---

## Day 9 — Deployment to Free-Tier Hosting

### 🎯 Objective
Deploy the full application (frontend, backend, database already on Atlas) to free-tier hosting so it's publicly accessible via a URL.

### 📖 What I'll learn
Environment-based configuration for production, deploying a Node/Express API and a React app separately, connecting them in production, CORS configuration for cross-origin deployed apps.

### 🛠 Features to build
- No new product features — deployment configuration only
- Production environment variables set on hosting platforms (not in code)
- Production CORS configuration (only allow the deployed frontend origin)

### 📝 Step-by-step implementation plan
1. **Guided manual step:** create a Render account (free tier), create a new Web Service from the GitHub repo's `/server` folder, set build command (`npm install`) and start command (`node server.js`), add environment variables (`MONGO_URI`, `JWT_SECRET`, `ANTHROPIC_API_KEY`) in Render's dashboard (never in code).
2. Confirm the backend is live and reachable at its Render URL (test the health-check route).
3. **Guided manual step:** create a Vercel (or Netlify) account, import the GitHub repo's `/client` folder, set the build output, and add an environment variable for the API base URL pointing to the Render backend URL.
4. Update frontend Axios base URL to use this environment variable instead of `localhost`.
5. Update backend CORS config to allow only the deployed frontend's exact URL (not `*`) for security.
6. Redeploy both after config changes; do a full manual walkthrough of the live app: signup, login, browse topics, submit a practice (text + voice), view results, check dashboard/history.
7. Confirm MongoDB Atlas network access allows connections from Render (0.0.0.0/0, already set Day 2, or restrict to Render's IPs if preferred).

### 📂 Files and folders to create or modify
```
/client/.env.production (VITE_API_URL=...)
/server (CORS config update in server.js)
README.md (add live demo link)
```

### 🔗 APIs, libraries, services, or tools to integrate
- Render (free web service hosting for backend)
- Vercel or Netlify (free hosting for frontend)
- MongoDB Atlas (already set up Day 2)

### 🧪 Testing tasks
- Full end-to-end walkthrough on the live public URL (not localhost), on both desktop and a mobile phone browser.
- Confirm voice input works on the live deployed site (not just localhost).
- Confirm no console errors related to CORS or mixed content (http/https) in production.
- Share the live link with one other person (classmate/friend) to sanity-check it works outside your own machine/network.

### 🐞 Common issues and debugging tips
- CORS errors in production: double-check the exact deployed frontend URL (including https and no trailing slash) is what's allowed in backend CORS config.
- Render free-tier cold start: the first request after inactivity can be slow — this is expected on free tier, not a bug; mention it if demoing live.
- Environment variable not picked up: confirm the variable name matches exactly what the code reads, and that you redeployed after adding it.

### ✅ End-of-day checklist
- [ ] Backend live on Render, reachable via public URL
- [ ] Frontend live on Vercel/Netlify, reachable via public URL
- [ ] Full user flow tested successfully on the live deployed app (not localhost)
- [ ] Live demo link added to GitHub README

### 📸 Expected project state and screenshots to capture
- Screenshot: Render dashboard showing the live backend service
- Screenshot: Vercel/Netlify dashboard showing the live frontend
- Screenshot: the live app running in a browser with the real public URL visible in the address bar

### ➡️ Handoff notes for Day 10
The app is fully live and functional. Day 10 is final polish, README/documentation, recording a demo, and packaging everything for sharing (LinkedIn, GitHub, interview-ready pitch).

---

## Day 10 — Final Polish, Documentation & Launch

### 🎯 Objective
Finalize documentation, record a demo, do a last quality pass, and package the project for public sharing (GitHub + LinkedIn) as a completed v1.0.

### 📖 What I'll learn
Writing a professional project README, presenting a technical project publicly, preparing an interview-ready project narrative.

### 🛠 Features to build
- No new features — documentation, demo recording, and final QA only

### 📝 Step-by-step implementation plan
1. Write a complete `README.md`: project description, problem/motivation (your own GD story), features list, tech stack, architecture diagram (simple text or image), setup instructions, live demo link, screenshots.
2. Do one final full walkthrough of the live app, fixing any last small visual issues found.
3. Record a short screen-capture demo (2-3 minutes): sign up, pick a topic, answer by voice, show AI feedback, show dashboard/streak. This becomes your LinkedIn post video and interview-ready demo.
4. Write your LinkedIn post using the pitch deck content (problem → solution → what you built → what you learned → link to live app + GitHub).
5. Do a final review of the PRD, blueprint, and pitch deck (all three deliverables from Day 1) to ensure the live product matches what was promised — note any intentional deviations honestly.
6. Prepare a short (30-60 second) verbal pitch of the project for interviews, grounded in your own GD-failure story and what the AI actually evaluates.

### 📂 Files and folders to create or modify
```
/README.md (final version)
/demo-video (or link to where it's hosted, e.g., LinkedIn/YouTube unlisted)
```

### 🔗 APIs, libraries, services, or tools to integrate
- None new.

### 🧪 Testing tasks
- Final live-app walkthrough with fresh eyes (or ask someone else to try it) — no critical bugs remaining.
- Confirm all links in the README (live demo, GitHub) actually work when clicked by someone else.

### 🐞 Common issues and debugging tips
- Overclaiming in the README: only describe what's actually built and live — list deferred items honestly under "Future Scope," which strengthens rather than weakens the story.
- Demo video shows a bug live: do a quick dry run before recording the final take.

### ✅ End-of-day checklist
- [ ] README complete with live demo link, screenshots, and setup instructions
- [ ] Demo video recorded
- [ ] LinkedIn post drafted and published
- [ ] Verbal project pitch practiced and ready for interviews
- [ ] v1.0 confirmed live, complete, and matching the PRD's Day-10 success definition

### 📸 Expected project state and screenshots to capture
- Screenshot: final GitHub README as rendered on GitHub
- Screenshot/recording: the demo video
- Screenshot: published LinkedIn post

### ➡️ Handoff notes (capstone complete)
GD Prep Coach v1.0 is live, deployed, tested, and documented. Any further work (audio/tone analysis, push notifications, live GD rooms, mentor review) belongs to a clearly separate "v2" effort and should not be treated as unfinished v1.0 work.
