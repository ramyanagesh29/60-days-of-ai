# Defend Your Experience 🛡️
### Day 50 of the ABTalks 60-Day Claude Challenge

An AI-powered adaptive interview simulator that stress-tests the claims on your resume, LinkedIn profile, or project write-up — the way a skeptical real interviewer would.

## 💡 The Idea

Most tools help you *polish* your resume. This one does the opposite: it treats every line you've written as a claim that needs to be **defended**, not just stated. It reads your material, pulls out every meaningful claim, and then interrogates you about it — one adaptive question at a time.

## ⚙️ How It Works

1. **Share your material** — paste your resume text, LinkedIn About section, project description, or performance review (drag-and-drop or paste)
2. **Claim extraction** — Claude reads the text and extracts every defensible claim (achievements, metrics, responsibilities, credentials), flagging each as *Strong*, *Vague*, or *Needs Scrutiny*
3. **Adaptive interview** — an AI interviewer asks a sharp follow-up question per claim. Every answer shapes the next question — vague answers get pushed harder, strong answers get deeper technical or behavioral probes
4. **Live confidence tracking** — a sidebar scores how well each claim is holding up in real time
5. **Defense Report** — a final breakdown of which claims are well-defended, partial, or weak, with a specific tip to strengthen each one before a real interview

## 🎯 Configurable Interview Modes

- **Audience**: Campus Recruiter/HR, Technical Interviewer, Hiring Manager, or Mixed Panel
- **Intensity**: Supportive, Standard, or Hostile/Stress mode

## 🛠️ Built With

- Vanilla HTML / CSS / JavaScript — zero external dependencies
- Anthropic Messages API called directly from the browser (Claude Sonnet 4.6)
- `localStorage` for session history
- Graceful retry/backoff handling for rate limits and transient API errors
- Fully responsive, single self-contained HTML file

## ✨ Key Features

- Drag-and-drop or paste-based intake
- Claim extraction with strength flags before the interview even starts
- Fully adaptive, non-templated follow-up questions generated from the user's own answers
- Per-claim confidence meter with live updates
- Exportable Defense Report (.txt) with full transcript
- Session history stored locally — revisit past interviews anytime
- Error banners with retry for temporary API failures — no dead ends

## 🚀 Try It

Open `defend-your-experience.html` in any browser (works as a Claude artifact too — no backend, no API key setup needed).

## 🎓 Why I Built This

Résumé lines are cheap. Interviewers know it — and they probe. This project came from a simple realization while prepping for placement season: it's not enough to *write* strong claims, you have to be able to *defend* them under pressure, with specifics, numbers, and ownership clearly separated from team effort. This tool is my own practice ground for that, built as Day 50 of my Claude Challenge.

## Screenshots

![Landing screen](./screenshots/Defend-Dashboard.png)
![Audience & intensity picker](./screenshots/Audience.png)
![Adaptive interview catching a contradiction](./screenshots/Experience.png)
![Full interview conversation](./screenshots/Conversation.png)
---
🔗 Connect: [LinkedIn](https://www.linkedin.com/in/ramya-n2918) | [GitHub](https://github.com/ramyanagesh29)

*Part of the ABTalks 60-Day Claude Challenge — Day 50 of 60*
