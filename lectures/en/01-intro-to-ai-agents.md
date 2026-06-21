# 01 — Intro to AI Agents

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](../de/01-intro-to-ai-agents.md)

## Concept

An **AI agent** is an LLM given three things a plain chatbot doesn't have:
1. A **role/goal** — a specific job, not "answer anything"
2. **Tools** — ways to act on the world (search the web, call an API, read a file) beyond just generating text
3. **Autonomy over a task** — it decides *how* to use its tools to reach its goal, rather than following a fixed script

A single LLM call answers one prompt. An agent can take multiple steps: think, call a tool, look at the result, decide what to do next, repeat until done.

## In this repo

Open [src/research_crew/crew.py](../../src/research_crew/crew.py). The `researcher` agent ([crew.py:17-23](../../src/research_crew/crew.py#L17-L23)) is a complete minimal example:

```python
@agent
def researcher(self) -> Agent:
    return Agent(
        config=self.agents_config['researcher'],
        verbose=True,
        tools=[SerperDevTool()]
    )
```

- Its **role/goal/backstory** come from [config/agents.yaml](../../src/research_crew/config/agents.yaml) — read that file. Notice `{topic}` is a placeholder filled in at runtime.
- Its **tool** is `SerperDevTool()` — without it, the agent could only use knowledge baked into the LLM at training time; with it, the agent can search the live web.
- Its **autonomy**: nobody tells it which search queries to run. Given the task description, it decides.

Run the crew with `verbose=True` already set, and watch the terminal (or the Streamlit demo) — you'll see the researcher agent thinking, choosing a search query, reading results, and deciding whether it has enough information yet.

## Exercise

1. Run the crew (`uv run research_crew`) with a topic of your choice (edit `inputs` in [main.py](../../src/research_crew/main.py)).
2. Read the verbose terminal output. Identify the exact moment the agent decides to call its tool, and the moment it decides it's done researching.
3. In your own words (a few sentences, no code), explain: what would be different if `researcher` had no tools at all? Would the agent still "do" anything, or just generate text once?

## Stretch goal

Temporarily remove `tools=[SerperDevTool()]` from the `researcher` agent and re-run. Compare the report quality/specificity to a run with the tool present. Put the tool back afterward.
