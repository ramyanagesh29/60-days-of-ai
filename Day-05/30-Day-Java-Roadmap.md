# 30-Day Java Learning Roadmap
### 1 hour/day · Beginner-friendly · Zero prior Java experience assumed

---

## How to use this roadmap
- Each day = ~1 hour: roughly 20 min reading/watching, 30 min hands-on coding, 10 min review.
- Do the days in order — each week builds on the last.
- Keep all your code in one folder/repo (e.g., `java-30-day-challenge`) so your progress is visible.
- Miss a day? Don't restart — just pick up where you left off.

**Setup (do this before Day 1, ~20 min):**
- Install [JDK 21 (Adoptium/Temurin)](https://adoptium.net/)
- Install [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download/) (free, beginner-friendly)
- Verify install: run `java -version` and `javac -version` in your terminal

---

## Week 1: Java Fundamentals
**Milestone:** Comfortable writing simple Java programs — variables, logic, loops, and methods.

| Day | Task | Resource |
|---|---|---|
| 1 | Write & run "Hello World"; understand `class`, `main`, compiling vs. running | [Oracle Java Tutorials — Getting Started](https://docs.oracle.com/javase/tutorial/getStarted/) |
| 2 | Variables, data types (`int`, `double`, `boolean`, `String`), type casting | W3Schools Java — Variables |
| 3 | Operators (arithmetic, comparison, logical) + simple calculator program | W3Schools Java — Operators |
| 4 | Conditionals: `if`, `else if`, `else`, `switch` | W3Schools Java — Conditions |
| 5 | Loops: `for`, `while`, `do-while` | W3Schools Java — Loops |
| 6 | Arrays: creation, iteration, common operations | W3Schools Java — Arrays |
| 7 | **Project:** Build a **Number Guessing Game** (random number, loop until guessed, hint if too high/low) | Use `java.util.Scanner` + `java.util.Random` |

---

## Week 2: Object-Oriented Programming (OOP)
**Milestone:** Understand and apply classes, objects, and the four OOP pillars.

| Day | Task | Resource |
|---|---|---|
| 8 | Classes & objects: fields, constructors, methods | [Oracle Tutorials — Classes & Objects](https://docs.oracle.com/javase/tutorial/java/javaOO/) |
| 9 | Encapsulation: private fields, getters/setters | Same Oracle OOP trail |
| 10 | Inheritance: `extends`, `super`, method overriding | Same Oracle OOP trail |
| 11 | Polymorphism & abstraction: abstract classes, interfaces | Same Oracle OOP trail |
| 12 | `ArrayList` and the Collections basics | [Baeldung — Java ArrayList Guide](https://www.baeldung.com/java-arraylist) |
| 13 | Exception handling: `try/catch/finally`, custom exceptions | W3Schools Java — Exceptions |
| 14 | **Project:** Build a **Library Management System** (console app: `Book` and `Member` classes, add/borrow/return books using an `ArrayList`) | Combine everything from Week 2 |

---

## Week 3: Core Java Deep Dive
**Milestone:** Work confidently with strings, collections, and file I/O; write cleaner, more idiomatic code.

| Day | Task | Resource |
|---|---|---|
| 15 | String methods & `StringBuilder` | W3Schools Java — Strings |
| 16 | `HashMap` and `HashSet` — when and why to use them | [Baeldung — Java HashMap Guide](https://www.baeldung.com/java-hashmap) |
| 17 | File I/O basics: reading/writing text files | [Baeldung — Java File Operations](https://www.baeldung.com/reading-file-in-java) |
| 18 | Static vs. instance members; the `this` keyword | Oracle Tutorials — Classes |
| 19 | Java naming conventions & clean code basics | [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html) |
| 20 | Intro to lambdas & streams (just the basics: `.filter()`, `.map()`, `.forEach()`) | [Baeldung — Java Streams Intro](https://www.baeldung.com/java-8-streams-introduction) |
| 21 | **Project:** Build an **Expense Tracker** (add/view/delete expenses, save/load from a text file, use `HashMap` for category totals) | Combine Week 3 concepts |

---

## Week 4: Real-World Skills & Capstone
**Milestone:** Understand testing, basic tooling, and ship one complete, polished project.

| Day | Task | Resource |
|---|---|---|
| 22 | Intro to unit testing with JUnit 5 | [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/) |
| 23 | Debugging in IntelliJ (breakpoints, step-through) | IntelliJ built-in docs (Help menu) |
| 24 | Intro to Maven or Gradle (project structure, dependencies) | [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) |
| 25 | Version control basics: Git init, commit, push to GitHub | [GitHub Docs — Git Basics](https://docs.github.com/en/get-started) |
| 26 | Plan your capstone project (see below) — outline classes & features | — |
| 27 | Capstone: build core logic | — |
| 28 | Capstone: add features + handle edge cases | — |
| 29 | Capstone: write 3–5 unit tests, polish, add a README | — |
| 30 | Capstone: final review, push to GitHub, write a short reflection on what you learned | — |

### Capstone Project (Days 26–30): **"Task Manager CLI"**
A command-line to-do list app that:
- Adds, edits, deletes, and lists tasks (with priority & due date)
- Marks tasks complete/incomplete
- Saves/loads tasks from a file so data persists between runs
- Includes at least 3 JUnit tests
- Has a clean `README.md` explaining how to run it

This project touches every skill from the roadmap: OOP, collections, file I/O, exceptions, and testing — a great portfolio piece.

---

## Final Outcome
By Day 30, you will be able to:
- Read and write idiomatic, object-oriented Java code
- Use core data structures (`ArrayList`, `HashMap`, arrays) confidently
- Handle errors gracefully with exceptions
- Read/write files and persist simple data
- Write basic unit tests
- Use Git/GitHub to track and share your work
- Show a completed, working Java project on your GitHub profile

**Next steps after Day 30:** Spring Boot (for web apps/APIs), Java Generics, multithreading, or a data structures & algorithms track (e.g., LeetCode "Easy" problems in Java).
