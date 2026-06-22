# Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](de/README.md)

These are the hands-on exercise sessions for **Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI**. Lecture theory is delivered via slides in class; this series is the practice companion, using this repository as the running example, and is deliberately scoped to the concepts that are actually demonstrated in this project's code rather than a comprehensive survey of every agentic-AI topic.

Every exercise session has the same two-part shape:
- **Part 1 — Theory**
  - **Concept** — what the idea is and why it matters
  - **Original paper** — the seminal paper (or book/spec) behind the concept, with a reproduced figure where one exists and is openly available
- **Part 2 — Practice**
  - **In this repo** — exactly where that concept already shows up in `research_crew`, with file/line references
  - **Task** — something you implement or modify yourself
  - **Stretch goal** (optional) — a harder follow-up if you finish early

You should have [Run the crew](../README.md#run-the-crew) working (via Codespaces or locally) before exercise 1.

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

Alongside the exercise sessions, teams design their own crew for a topic of their choice, growing it in complexity milestone-by-milestone as new exercise content unlocks new capabilities, with a critical risk/constraint analysis as the main graded deliverable and working code as an optional bonus. See [Assignment Overview](en/assignment-overview.md), [Assignment Milestones](en/assignment-milestones.md), and [Assignment Templates](en/assignment-templates.md).

## For instructors

Each exercise references real files in `src/research_crew/`. Have students work directly in their own Codespace or fork — see the main [README](../README.md) for the two setup options. Solutions aren't included on purpose; if you want a reference implementation for grading, ask students to open a PR against their own fork so you can review the diff. For the team assignment specifically, see the "For instructors" section in the [Assignment Overview](en/assignment-overview.md#for-instructors) for repo/team setup.
