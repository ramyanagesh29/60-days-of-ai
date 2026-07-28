# Day 27 – Interactive Storytelling with Claude

## Prior Authorization Story Simulator

For Day 27 of the #60DayClaudeChallenge, I built an interactive Prior Authorization Story Simulator using Claude.

The goal was to turn a complex healthcare workflow into a beginner-friendly interactive story using conversations, choices, and visual progress.

## Story Overview

The simulator follows Rahul, a patient diagnosed with Rheumatoid Arthritis, through the Prior Authorization journey for Humira.

Priya, a healthcare operations specialist, explains each stage of the process in simple language while the user makes choices and progresses through the story.

The story contains 8 scenes:

1. Doctor Visit
2. Insurance Roadblock
3. What is Prior Authorization?
4. Insurance Review
5. Denial
6. Appeal
7. Approval
8. Final Takeaways

## Features

- Interactive healthcare storytelling
- 8-scene Prior Authorization journey
- Rahul and Priya conversational interface
- Two choices after each scene
- Dynamic story progression
- Progress bar
- Beginner-friendly PA explanations
- Denial and appeal workflow
- Approval journey
- Patient and healthcare-system perspectives
- Restart option to explore different dialogue paths
- Responsive web interface

## Screenshots

### 1. Story Beginning

Rahul begins his healthcare journey after visiting City Medical Center and receiving a diagnosis and treatment recommendation.

![Story Start](screenshots/story-start.png)

### 2. Understanding Prior Authorization

Priya explains Prior Authorization and why insurance review can affect access to treatment.

![PA Explanation](screenshots/pa-explanation.png)

### 3. Denial and Appeal Journey

The request is denied because step therapy documentation is missing. The story demonstrates that a denial is not necessarily the end of the process and shows how an appeal can be prepared.

![Denial and Appeal](screenshots/denial-appeal.png)

### 4. Approval and Final Takeaways

The story progresses through approval and concludes with lessons from both the patient and healthcare-system perspectives.

![Approval and Takeaways](screenshots/approval-takeaways.png)

## Key Takeaways

Through this simulation, I learned that Prior Authorization involves more than submitting a request and waiting for approval.

The payer may review eligibility, clinical documentation, diagnosis information, and step therapy history.

I also learned that a denial does not always mean treatment is permanently rejected. Missing documentation can lead to an appeal process involving additional records and a Letter of Medical Necessity.

The story also demonstrates how delays and administrative work can affect both patients and healthcare providers.

## What I Learned

### Interactive Storytelling

Complex concepts can be easier to understand when they are presented through characters, conversations, and decisions rather than only static information.

### Conversational UI

I learned how a chat-style interface can guide users through an educational experience while maintaining a clear progression.

### JavaScript Interaction

The project demonstrates dynamic scene progression, user choices, progress tracking, and updating the conversation interface using JavaScript.

### Healthcare Workflow

I gained a better understanding of the stages involved in a Prior Authorization journey, including request submission, payer review, denial, appeal, and approval.

## Technologies Used

- HTML
- Tailwind CSS
- Vanilla JavaScript
- Claude

## Challenge

Day 27 – Interactive Storytelling with Claude

#60DayClaudeChallenge
