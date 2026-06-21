# 07 — Planning Pattern

## Concept

Instead of an agent improvising step-by-step, a **planner** first produces an explicit plan — a sequence of steps — before any task executes. This trades a bit of latency/cost up front for more predictable, reviewable execution: you can read the plan and catch a bad approach before the agent burns tool calls and tokens on it.

## In this repo

CrewAI builds this in at the `Crew` level via two fields (`crew.py` doesn't use them yet):

```python
return Crew(
    agents=self.agents,
    tasks=self.tasks,
    process=Process.sequential,
    verbose=True,
    planning=True,
    planning_llm="gemini/gemini-2.5-flash",
)
```

When `planning=True`, CrewAI runs an internal `AgentPlanner` (using `planning_llm`) before execution starts, which adds a plan to each task's context.

## Exercise

1. Add `planning=True` and `planning_llm="gemini/gemini-2.5-flash"` to the `Crew` in [crew.py](../src/research_crew/crew.py).
2. Re-run the crew with verbose output and find the planning step in the logs — it happens before `research_task` starts. Read the generated plan.
3. Compare two runs of the same topic, one with `planning=True` and one without. Does the plan visibly change *what* the researcher searches for, or just add overhead with no behavior change? Write down your observation — there's no single right answer, the point is to actually look.

## Stretch goal

Planning costs an extra LLM call before any task runs. For a 2-task crew like this one, is that overhead worth it? Argue both sides in a few sentences, then think about when a crew has enough tasks/agents that planning would clearly start paying for itself (hint: think about lecture 08's multi-agent crews).
