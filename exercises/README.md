# Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](de/README.md)

These are the hands-on sprints for **Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI**. Lecture theory is delivered via slides in class; this series is the practice companion, using this repository's demo crew as the running example — and it's also the graded team assignment, not a separate thing alongside it. Every sprint is something you do directly on **your own use case**, not a generic exercise you do once and then redo for real later.

Each sprint has the same shape:
- **Background** — just enough theory to place the concept, citing its seminal paper (with the original figure, where one exists)
- **In this repo** — exactly where the concept shows up in the demo crew's code, with file/line references
- **Your task** — sprint planning (open GitHub Issues as user stories/epics) and concrete steps for *your* crew, ending with a few pointed questions you answer directly in `DESIGN.md`
- **Stretch goal** (optional) — a harder follow-up if you finish early

You should have [Run the crew](../README.md#run-the-crew) working in **your team's own repo** before Sprint 0 — see the main [README's "Getting access"](../README.md#getting-access-students) section if you don't have that yet.

Lakshmanan's *Generative AI Design Patterns* is cited as a companion text in Sprint 5; Simon (1969) and Brown (2008) ground the design-thinking elements in Sprint 0; all other citations are specific arXiv papers, listed per sprint.

## Sprints

| # | Title | Unlocks |
| --- | --- | --- |
| [0](en/00-vision-architecture.md) | Vision & Architecture | Pick your use case, design your agents and tasks |
| [1](en/01-first-mvp.md) | First Runnable MVP | A working sequential (or parallel) crew |
| [2](en/02-tools.md) | Tools | A tool your use case actually needs |
| [3](en/03-rag.md) | RAG | Grounded answers from a real knowledge source *(interim submission due)* |
| [4](en/04-dynamic-orchestration.md) | Dynamic Orchestration (Hierarchical) | A third agent + manager-delegated process |
| [5](en/05-production-safety.md) | Production Safety & Stability | Threat model, monitoring plan *(final submission due)* |

For what's graded and how, the submission package, team setup, and templates (`DESIGN.md`, `TEAM.md`, user stories, peer evaluation), see [Assignment Overview](en/assignment-overview.md) (English / [Deutsch](de/assignment-overview.md)).

## Learn more on your own

Each sprint's "Background" section gives you just enough to place the concept — for everything CrewAI itself can do beyond what this repo's demo crew demonstrates, go straight to the source:
- [CrewAI documentation](https://docs.crewai.com) — the full concept reference (agents, tasks, processes, tools, memory, knowledge, flows) and the [quickstart](https://docs.crewai.com/en/quickstart)
- [Multi AI Agent Systems with crewAI](https://www.deeplearning.ai/short-courses/multi-ai-agent-systems-with-crewai/) (DeepLearning.AI) — a short video course taught by CrewAI's founder; free during DeepLearning.AI's platform beta, may not stay free indefinitely

## For instructors

Each sprint references real files in `src/research_crew/`. Students work in their own team's repo (one per team, provisioned from this template under your course organization) — see the main [README's "Getting access"](../README.md#getting-access-students) for the student-facing enrollment flow, and the "For instructors" section in the [Assignment Overview](en/assignment-overview.md#for-instructors) for the full org/team/repo provisioning and the automated sign-up workflow. Solutions aren't included on purpose; review submissions by checking each team's merged sprint pull requests directly.
