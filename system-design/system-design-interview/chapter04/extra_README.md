# Chapter 1: A Framework for System Design Interviews

## Introduction

A system design interview asks you to turn an ambiguous problem into a design that meets agreed requirements. The interviewer evaluates how you ask questions, explain decisions, work through trade-offs, and respond to feedback, as well as your technical knowledge.

The aim is to demonstrate a sound design process within limited time. Alex Xu's four-step framework gives the discussion a useful structure:

1. Understand the problem and establish design scope.
2. Propose a high-level design and get buy-in.
3. Design deep dive.
4. Wrap-up.

This is Chapter 1 in our study sequence. In *System Design Interview: An Insider's Guide*, Volume 1, this material is Chapter 3.

## Step 1: Understand the Problem and Establish Design Scope

### Goal

Agree on what the system must do and the constraints it must satisfy before choosing an architecture. A technically impressive design can still solve the wrong problem.

### Approach

- Clarify the essential features and what is outside the scope.
- Ask about user counts, traffic, and expected growth.
- Establish which platforms the system serves and any existing technology or service constraints.
- Record the interviewer's answers. If asked to make an assumption, state it explicitly and write it down so it can be revisited.

### Example: News Feed

Useful questions include:

- Are we supporting web, mobile, or both?
- Does the scope include creating posts and viewing friends' posts?
- Should newer posts appear first, or does the feed need a ranking system?
- How many friends can each user have, and how many users are active daily?
- Can posts contain images and videos?

In the book's example, the agreed scope includes both platforms, a feed ordered from newest to oldest, up to 5,000 friends per user, 10 million daily active users, and media posts. These are assumptions for that example; establish the requirements afresh for each problem.

## Step 2: Propose High-Level Design and Get Buy-In

### Goal

Develop an overall architecture and check with the interviewer that it addresses the agreed problem. Getting buy-in means reaching agreement on the direction before spending time on details.

### Approach

- Sketch the main components and show how requests and data move between them. Depending on the requirements, these may include clients, APIs, servers, databases, caches, a content delivery network (CDN), or queues.
- Explain each component's responsibility and invite feedback as you build the diagram.
- Use rough capacity estimates when they help check whether the design can support the required scale. Agree on whether calculations are useful before spending time on them.
- Walk through concrete use cases to check the flow and uncover missing behavior or edge cases.
- Agree on the appropriate level of detail for APIs and database schemas; this depends on the problem's scope.

### Example: Two News Feed Flows

Separate the discussion into two user actions:

1. **Publishing a post:** Save the post and make it available in friends' feeds.
2. **Retrieving a feed:** Assemble and return the relevant friends' posts, newest first.

The book's example diagrams show one possible architecture for these flows. The detailed design is covered in [Design a News Feed System](../chapter12).

**Feed publishing:**

![High-level feed publishing flow](../chapter04/images/feed-publishing.png)

**Feed retrieval:**

![High-level news feed retrieval flow](../chapter04/images/news-feed-building.png)

## Step 3: Design Deep Dive

### Goal

Explain how the most important parts of the proposed system work, including their bottlenecks and trade-offs.

### Approach

- Confirm that the goals, scope, and overall architecture are agreed before going deeper.
- Choose the components to examine with the interviewer, using their feedback and the problem's requirements to set priorities.
- Trace the relevant data flow and discuss where performance or reliability could become a problem.
- Explain the alternatives and why a choice fits the constraints.
- Keep the remaining time in view. Spend detail where it helps evaluate the design.

### Example Topics

- **URL shortener:** How long URLs map to short identifiers, including the hash design if that is the chosen approach.
- **Chat system:** Message delivery latency and handling online/offline status.
- **News feed:** The work involved in publishing posts and retrieving a user's feed.

The news feed example expands the earlier flows into more detailed components:

**Feed publishing deep dive:**

![Detailed feed publishing flow](../chapter04/images/feed-publishing-deep-dive.png)

**Feed retrieval deep dive:**

![Detailed news feed retrieval flow](../chapter04/images/news-feed-building-deep-dive.png)

## Step 4: Wrap-Up

### Goal

Leave the interviewer with a clear understanding of the design, its limitations, and the next improvements you would investigate.

### Approach

- Recap the final architecture and the reasons behind the main decisions, especially if you discussed several alternatives.
- Identify likely bottlenecks and explain how you would address them.
- Discuss failure cases such as a server going down or a network connection being lost.
- Cover relevant operational concerns: monitoring, error logs, and rolling out changes.
- Explain what might need to change at the next scale, such as growing from 1 million to 10 million users.
- Name useful follow-up work if more time were available, and respond to the interviewer's remaining questions.

## Best Practices

### Dos

- Make assumptions visible and check them against the requirements.
- Explain your reasoning throughout the discussion.
- Treat the interviewer as a collaborator and seek feedback early.
- Compare plausible alternatives and adjust when new information changes the problem.
- Prioritize the components that matter most to the system's goals.
- Ask for a hint when stuck and use it to keep the discussion moving.

### Don'ts

- Start selecting technologies before understanding the problem.
- Spend the opening minutes on one component's implementation details.
- Add complexity without explaining which requirement it serves.
- Work silently or defend a choice without considering feedback.
- Treat the first diagram as the end of the interview; allow time for refinement and follow-up questions.

## Time Management

The book gives these rough ranges for a 45-minute interview:

| Step | Suggested time |
| --- | --- |
| Understand the problem and establish scope | 3-10 minutes |
| Propose the high-level design and get buy-in | 10-15 minutes |
| Design deep dive | 10-25 minutes |
| Wrap-up | 3-5 minutes |

These are flexible ranges, not four fixed allocations to add together. Adapt the time to the problem and the interviewer's priorities while reserving time for the wrap-up. For practice, one possible 45-minute allocation is **7 + 12 + 22 + 4 minutes**.

## Sources

- Alex Xu, *System Design Interview: An Insider's Guide*, Volume 1, Chapter 3, "A Framework for System Design Interviews" (supplied PDF, pages 42-50). The framework, example assumptions, timing ranges, and existing diagrams above come from this chapter.
- [ByteByteGo: System Design Interview Books - Volume 1 vs Volume 2](https://blog.bytebytego.com/p/system-design-interview-books-volume), which lists the book's chapter order.
- [liquidslr/system-design-notes: System Design Framework](https://github.com/liquidslr/system-design-notes/blob/main/03.%20System%20Design%20Framework/Readme.md), the example outline supplied by the user and used as an organizational reference. These notes summarize the material in our own wording.

[Back to the study index](../README.md)
