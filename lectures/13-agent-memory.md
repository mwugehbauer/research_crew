# 13 — Agent Memory

## Concept

Memory lets an agent retain information *across* runs (or across tasks within a run) instead of starting from a blank slate every time. CrewAI distinguishes several kinds:
- **Short-term memory** — recent context within the current crew run
- **Long-term memory** — persisted across separate runs (e.g. "we researched this topic last week")
- **Entity memory** — facts about specific entities (people, organizations) the crew has encountered

This is different from RAG (lecture 05): RAG retrieves from documents you provided; memory retrieves from what the *crew itself* has previously said or learned.

## In this repo

Memory is currently off — when we printed the crew object earlier in this project's setup, it showed `memory=False`, `short_term_memory=None`, `long_term_memory=None`, `entity_memory=None`. Turning it on is a one-line change to [crew.py](../src/research_crew/crew.py):

```python
return Crew(
    agents=self.agents,
    tasks=self.tasks,
    process=Process.sequential,
    verbose=True,
    memory=True,
)
```

Like knowledge sources (lecture 05), memory also embeds content under the hood — so the same Gemini-embedder gotcha applies. Pass `embedder` (already configured in this crew) and it'll be reused for memory too.

## Exercise

1. Set `memory=True` on the `Crew` and re-run the crew twice in the same process for the *same* topic (e.g. run it from a script that calls `.kickoff()` twice, or run `uv run research_crew` twice without restarting — note CrewAI memory persists to local storage between CLI invocations too, since it's disk-backed).
2. Check `~/.local/share/crewai` or wherever CrewAI's memory storage path resolves (the CLI/verbose logs usually show it) — look for memory files written.
3. Run the crew on a topic that overlaps with a previous one (e.g. "Artificial Intelligence in Healthcare" then "Artificial Intelligence in Drug Discovery") and see if anything in the verbose log shows the agent referencing memory from the earlier run.

## Stretch goal

Memory persists indefinitely by default — for a class where many students share one set of memory storage paths (unlikely with separate Codespaces, but possible locally), this could leak information between runs. Look up how to scope/reset CrewAI memory (hint: `crew.reset_memories()` or deleting the storage directory) and explain when you'd want to do that in a real classroom setting.
