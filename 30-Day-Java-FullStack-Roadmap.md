# 30-Day Java Full Stack Developer Roadmap
### For: Student · 1 hour/day · Mix of videos, projects, and reading

**A quick honest note before you start:** "Full Stack" is a big goal, and 1 hour/day for 30 days (≈30 hours total) is enough to build a *real, working full-stack app* and understand how the pieces connect — not enough for deep mastery of Java, Spring, or a frontend framework. Think of this as **Foundation Sprint 1**: you'll come out able to build and explain a simple full-stack project, with a clear map of what to learn next.

**Assumption:** Since you didn't specify prior experience, this assumes you're comfortable with basic programming logic (variables, loops, functions) but new to Java, Spring Boot, and web development. Tell me if that's off and I'll adjust.

---

## Setup (before Day 1, ~30 min)
- Install [JDK 21](https://adoptium.net/) and [IntelliJ IDEA Community](https://www.jetbrains.com/idea/download/)
- Install [VS Code](https://code.visualstudio.com/) (for frontend work) and [Node.js](https://nodejs.org/)
- Create a GitHub account + one repo: `java-fullstack-30day`
- Bookmark [Spring Initializr](https://start.spring.io/)

---

## Week 1: Java Core + OOP
**Milestone:** Write clean, object-oriented Java and understand how backend logic is structured.

| Day | Task | Resource (mixed style) |
|---|---|---|
| 1 | Java basics: syntax, variables, types, `Scanner` input | 📺 [Bro Code Java Full Course](https://www.youtube.com/watch?v=xk4_1vDrzzo) (first 30 min) |
| 2 | Conditionals & loops — build a small quiz program | 📖 W3Schools Java — Conditions/Loops |
| 3 | Arrays & `ArrayList` | 📺 Bro Code (continue) |
| 4 | Classes, objects, constructors | 📖 [Oracle OOP Trail](https://docs.oracle.com/javase/tutorial/java/javaOO/) |
| 5 | Inheritance, interfaces, `this`/`super` | 📖 Same Oracle trail |
| 6 | Exception handling (`try/catch`) | 📖 W3Schools Java — Exceptions |
| 7 | 🛠️ **Project:** Console **Student Grade Manager** (add students, grades, compute averages using OOP + `ArrayList`) | — |

---

## Week 2: Backend with Spring Boot
**Milestone:** Build and test a working REST API backed by a database.

| Day | Task | Resource |
|---|---|---|
| 8 | What is Spring Boot? Create a project via Spring Initializr, run "Hello World" endpoint | 📺 [Spring Boot Tutorial – Amigoscode](https://www.youtube.com/watch?v=9SGDpanrc8U) |
| 9 | REST basics: `@RestController`, `@GetMapping`, `@PostMapping` | 📖 [Baeldung — Spring Boot REST](https://www.baeldung.com/spring-boot-start) |
| 10 | Request/response bodies, DTOs, path/query params | 📖 Baeldung (continue) |
| 11 | Intro to databases: connect Spring Boot to H2 (in-memory) via Spring Data JPA | 📺 Amigoscode video (continue) |
| 12 | CRUD operations: Create, Read, Update, Delete via JPA repository | 📖 [Spring Data JPA Guide](https://spring.io/guides/gs/accessing-data-jpa/) |
| 13 | Testing your API with Postman | 📺 [Postman Beginner Guide](https://www.youtube.com/results?search_query=postman+beginner+tutorial) |
| 14 | 🛠️ **Project:** **Task Manager REST API** (CRUD endpoints for tasks: title, status, due date; stored in H2) | Builds directly on Days 8–13 |

---

## Week 3: Frontend Basics + Connecting to Backend
**Milestone:** Build a simple interactive UI that talks to your Spring Boot API.

| Day | Task | Resource |
|---|---|---|
| 15 | HTML fundamentals: structure, forms, tables | 📖 [MDN HTML Basics](https://developer.mozilla.org/en-US/docs/Learn/HTML) |
| 16 | CSS fundamentals: layout, flexbox basics | 📺 [Kevin Powell — Flexbox Crash Course](https://www.youtube.com/watch?v=JJSoEo8JSnc) |
| 17 | JavaScript fundamentals: variables, functions, DOM manipulation | 📖 [MDN JavaScript Basics](https://developer.mozilla.org/en-US/docs/Learn/JavaScript) |
| 18 | `fetch()` API: calling a REST endpoint from JavaScript | 📖 [MDN — Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) |
| 19 | Enabling CORS in Spring Boot so frontend can call it | 📖 [Baeldung — CORS in Spring](https://www.baeldung.com/spring-cors) |
| 20 | Build a simple form UI that POSTs data to your Task API | Combine Days 15–19 |
| 21 | 🛠️ **Project:** Connect your **Task Manager UI** (HTML/CSS/JS) to the **Task Manager API** — full add/view/complete/delete flow working end-to-end | Your first real full-stack loop |

---

## Week 4: Polish, Git, and Capstone
**Milestone:** Ship one complete, presentable full-stack project.

| Day | Task | Resource |
|---|---|---|
| 22 | Git & GitHub: commits, branches, `.gitignore`, pushing a full project | 📖 [GitHub Docs — Git Basics](https://docs.github.com/en/get-started) |
| 23 | Basic input validation (backend `@Valid`, frontend form checks) | 📖 [Baeldung — Spring Validation](https://www.baeldung.com/spring-boot-bean-validation) |
| 24 | Error handling: meaningful API error responses, showing errors in UI | 📖 [Baeldung — Exception Handling in Spring](https://www.baeldung.com/exception-handling-for-rest-with-spring) |
| 25 | Plan capstone: sketch features, entities, API endpoints, pages needed | — |
| 26 | Capstone: backend (entities + endpoints) | — |
| 27 | Capstone: frontend (pages + API calls) | — |
| 28 | Capstone: connect everything, handle edge cases | — |
| 29 | Capstone: styling pass + write README (setup instructions, screenshots) | — |
| 30 | Final review, push to GitHub, record a 2-min demo video/GIF for your portfolio | — |

### Capstone Project (Days 25–30): **"Personal Expense Tracker"**
Full-stack app with:
- **Backend:** Spring Boot + JPA + H2, CRUD endpoints for expenses (amount, category, date, note)
- **Frontend:** HTML/CSS/JS page to add expenses, list them, filter by category, show a running total
- **Extras if time allows:** category-wise totals, simple bar chart with Chart.js
- Pushed to GitHub with a clear README — this becomes your first full-stack portfolio piece

---

## Final Outcome
By Day 30, you will be able to:
- Write clean, object-oriented Java code
- Build a REST API with Spring Boot and connect it to a database
- Build a basic frontend with HTML/CSS/JS and connect it to a live API
- Understand the full request → backend → database → response → UI loop
- Use Git/GitHub to manage and showcase projects
- Show **two working full-stack-adjacent projects** on GitHub (Task Manager + Expense Tracker)

**Next steps after Day 30 (Sprint 2 ideas):** Spring Security (authentication/login), a proper frontend framework (React), deploying to the cloud (Render/Railway), and Java DSA practice for interviews.
