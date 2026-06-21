# Agentic AI Lecture Series — built on research_crew

This series teaches agentic AI concepts using this repository as the running example. It follows the structure of Microsoft's [AI Agents for Beginners](https://github.com/microsoft/ai-agents-for-beginners) course, adapted to CrewAI and grounded entirely in this project's code instead of abstract examples.

Every lecture has the same shape:
- **Concept** — what the idea is and why it matters
- **In this repo** — exactly where that concept already shows up in `research_crew`, with file/line references
- **Exercise** — something students implement or modify themselves
- **Stretch goal** (optional) — a harder follow-up for students who finish early

Students should have [Run the crew](../README.md#run-the-crew) working (via Codespaces or locally) before lecture 1.

## Sessions

| # | Title | Maps to AI Agents for Beginners |
| --- | --- | --- |
| [00](00-course-setup.md) | Course Setup | 00-course-setup |
| [01](01-intro-to-ai-agents.md) | Intro to AI Agents | 01-intro-to-ai-agents |
| [02](02-agentic-frameworks.md) | Agentic Frameworks: CrewAI Basics | 02-explore-agentic-frameworks |
| [03](03-agentic-design-patterns.md) | Agentic Design Patterns | 03-agentic-design-patterns |
| [04](04-tool-use.md) | Tool Use | 04-tool-use |
| [05](05-agentic-rag.md) | Agentic RAG | 05-agentic-rag |
| [06](06-trustworthy-agents.md) | Building Trustworthy Agents | 06-building-trustworthy-agents |
| [07](07-planning-pattern.md) | Planning Pattern | 07-planning-design |
| [08](08-multi-agent-pattern.md) | Multi-Agent Pattern | 08-multi-agent |
| [09](09-metacognition.md) | Metacognition | 09-metacognition |
| [10](10-production.md) | AI Agents in Production | 10-ai-agents-production |
| [11](11-agentic-protocols.md) | Agentic Protocols (MCP/A2A) | 11-agentic-protocols |
| [12](12-context-engineering.md) | Context Engineering | 12-context-engineering |
| [13](13-agent-memory.md) | Agent Memory | 13-agent-memory |
| [14](14-securing-agents.md) | Securing AI Agents | 18-securing-ai-agents |

Not covered: the source course's "Microsoft Agent Framework" and "Browser-use / Computer Use Agents" modules are framework-specific to tools outside CrewAI's scope and are intentionally omitted.

## For instructors

Each exercise references real files in `src/research_crew/`. Have students work directly in their own Codespace or fork — see the main [README](../README.md) for the two setup options. Solutions aren't included on purpose; if you want a reference implementation for grading, ask students to open a PR against their own fork so you can review the diff.
