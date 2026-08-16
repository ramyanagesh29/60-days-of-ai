# 🤖 Autonomous Agent Studio

A single-file, browser-based multi-agent orchestration system that autonomously writes, evaluates, critiques, and improves code — with **zero backend** and live calls to the Claude API.

Built as part of the **ABTalks 60-Day Claude Challenge (Day 46)**.

![Status](https://img.shields.io/badge/status-working-brightgreen) ![Type](https://img.shields.io/badge/type-single--file--HTML-blue) ![No Backend](https://img.shields.io/badge/backend-none-purple)

## 🎯 What It Does

Give it a function/algorithm spec (e.g. *"write a debounce function with a leading-edge option"*), and a pipeline of **7 specialized AI agents** collaborate — live, in a real loop — to produce a polished, reviewed implementation.

Unlike a typical "chatbot writes code once" demo, this runs a genuine **evaluate → critique → improve** cycle with **no pre-set number of rounds**. The loop keeps going until a deterministic stop condition fires.

## 🧩 The Agents

| Agent | Role |
|---|---|
| 📋 **Planner** | Designs the implementation approach from the raw spec (runs once) |
| ⚡ **Executor** | Writes the first working code draft (runs once) |
| 📈 **Evaluator** | Scores the draft 0–10 on correctness, quality & efficiency (every round) |
| 🔍 **Critic** | Identifies specific, actionable weaknesses (every round) |
| 🛠️ **Improver** | Rewrites the code using eval + critique + memory (every round, unless stopped) |
| 🧠 **Memory Manager** | Condenses each round into a running lessons-learned log |
| ✅ **Final Reviewer** | Signs off once the loop stops, confirms production-readiness |

## 🔁 The Loop — Not a Fixed Pipeline

Every round makes **live API calls** to Claude — no hardcoded sequence, no canned scores. A deterministic **Stop-Check** runs after every round, in order:

1. **Plateau** — score improved less than a small delta for 2 straight rounds
2. **Threshold** — score crossed the target set at configuration time
3. **Hard cap** — safety fallback only, not the intended ending

Whichever condition fires first ends the loop and branches to the Final Reviewer.

## 📊 Dashboard Features

- Live animated workflow diagram (real cycle, not a straight pipeline)
- Active agent highlighting + status bar
- Round-by-round evaluation history with score deltas
- Real-time activity log
- Intermediate code outputs (plan → draft v0 → each revision)
- Memory panel showing accumulated cross-round lessons
- Final summary with execution stats, agent performance breakdown, and exact stop reason
- Retry handling and graceful failure recovery for API errors

## 🛠️ Tech Stack

- **Vanilla HTML/CSS/JS** — no frameworks, no build step, no dependencies
- Direct `fetch` calls to `https://api.anthropic.com/v1/messages`
- Model: `claude-sonnet-4-6`
- Fully self-contained single file — open it and run

## 🚀 How to Run

1. Download `autonomous-agent-studio.html`
2. Open it in any modern browser
3. Enter a function/algorithm spec, set your target quality score, plateau sensitivity, and hard cap
4. Click **Run Autonomous Pipeline** and watch the agents work in real time

## 💡 Key Design Decisions

- **Stop condition over round count**: the hardest part wasn't building the agents — it was designing a principled exit strategy so the loop doesn't run forever or stop too early.
- **State threads forward**: each Improver call receives the prior round's full evaluation + critique + memory, so the system doesn't "forget" earlier feedback.
- **Every output is real**: no regex-based scoring or canned text — every score, critique, and report shown is literal model output from that round's API call.

## 🔮 Extension Ideas

- Add a **Safety Monitor** agent to flag insecure code patterns in parallel with the Evaluator
- Extend to multi-file/project scope with a dependency-aware Planner
- Replace self-reported Evaluator scoring with a real sandboxed test runner
- Add a human-in-the-loop approval gate before Final Reviewer
- Persist Memory Manager notes across sessions via localStorage

## 📅 Part of

**ABTalks 60-Day Claude Challenge** — Day 46 
Building daily Claude-powered tools + documenting the process.

- LinkedIn: [ramya-n2918](https://linkedin.com/in/ramya-n2918)
- GitHub: [ramyanagesh29](https://github.com/ramyanagesh29)
