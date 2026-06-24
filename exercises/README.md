# Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](de/README.md)

These are the hands-on exercise sessions for **Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI**. Lecture theory is delivered via slides in class; this series is the practice companion, using this repository as the running example, and is deliberately scoped to the concepts that are actually demonstrated in this project's code rather than a comprehensive survey of every agentic-AI topic.

Every exercise session starts directly with the practical work rather than a separate theory block — it weaves in just enough background from the relevant paper (a short citation and, where one exists, its original figure) to place the concept, then goes straight into the code:
- **In this repo** — exactly where the concept already shows up in `research_crew`, with file/line references
- **Task** — something you implement or modify yourself
- **Stretch goal** (optional) — a harder follow-up if you finish early

This series doesn't repeat the lecture's own treatment of each topic — it's the hands-on companion, not a second lecture.

You should have [Run the crew](../README.md#run-the-crew) working in **your team's own repo** (via Codespaces or locally) before exercise 1 — see the main [README's "Getting access"](../README.md#getting-access-students) section if you don't have that yet.

Lakshmanan's *Generative AI Design Patterns* is cited as a companion text in exercise 05 (production); all other citations are specific arXiv papers, listed per exercise under "Original paper."

## Exercise Sessions

| # | Title |
| --- | --- |
| [00](en/00-course-setup.md) | Course Setup |
| [01](en/01-agentic-frameworks.md) | Agentic Frameworks: CrewAI Basics |
| [02](en/02-tool-use.md) | Tool Use |
| [03](en/03-agentic-rag.md) | Agentic RAG |
| [04](en/04-multi-agent-pattern.md) | Multi-Agent Pattern |
| [05](en/05-production.md) | AI Agents in Production |
| [06](en/06-securing-agents.md) | Securing AI Agents |

## Graded team assignment

Alongside the exercise sessions, teams design their own crew for a topic of their choice, growing it in complexity milestone-by-milestone as new exercise content unlocks new capabilities, with a critical risk/constraint analysis as the main graded deliverable and working code as an optional bonus. See [Assignment Overview](en/assignment-overview.md), [Assignment Milestones](en/assignment-milestones.md), [Assignment Templates](en/assignment-templates.md), and the [Sprint Plan](en/assignment-sprint-plan.md) for running it as Scrum.

## For instructors

Each exercise references real files in `src/research_crew/`. Students work in their own team's repo (one per team, provisioned from this template under your course organization) — see the main [README's "Getting access"](../README.md#getting-access-students) for the student-facing enrollment flow, and the "For instructors" section in the [Assignment Overview](en/assignment-overview.md#for-instructors) for the full org/team/repo provisioning and the automated sign-up workflow. Solutions aren't included on purpose; review submissions by checking each team's commit history directly.
