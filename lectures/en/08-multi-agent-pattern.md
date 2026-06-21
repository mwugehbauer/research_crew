# 08 — Multi-Agent Pattern

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](../de/08-multi-agent-pattern.md)

## Concept

Beyond a fixed sequential pipeline, CrewAI offers **hierarchical** orchestration: a manager agent (or manager LLM) decides which worker agent should handle each task, and in what order, rather than you hardcoding the sequence. This is the "multi-agent" pattern proper — agents whose collaboration is itself dynamic, not just a fixed pipe.

Tradeoff: more flexible, but less predictable and more expensive (the manager makes extra LLM calls to delegate).

## In this repo

Currently `process=Process.sequential` with exactly two agents in a fixed order ([crew.py:50](../../src/research_crew/crew.py#L50)). To go hierarchical, CrewAI requires either `manager_llm` or `manager_agent`:

```python
return Crew(
    agents=self.agents,
    tasks=self.tasks,
    process=Process.hierarchical,
    manager_llm="gemini/gemini-2.5-flash",
    verbose=True,
)
```

## Exercise

1. Add a third agent to [crew.py](../../src/research_crew/crew.py) and [config/agents.yaml](../../src/research_crew/config/agents.yaml) — an `editor` whose job is to proofread/polish the analyst's report for tone and clarity.
2. Add a corresponding `editing_task` in [config/tasks.yaml](../../src/research_crew/config/tasks.yaml) with `context: - analysis_task`.
3. Switch `process` to `Process.hierarchical` and add `manager_llm`. Remove the `agent:` field from each task in `tasks.yaml` — in hierarchical mode, the manager assigns tasks to agents dynamically rather than reading a fixed assignment.
4. Run it and watch the verbose logs: which agent does the manager pick for each task, and does it match what you'd expect from each agent's role?

## Stretch goal

Try `manager_agent` instead of `manager_llm` — define your own dedicated manager `Agent` with a role like "Editorial Director" and pass it in instead. Compare whether the delegation decisions change.
