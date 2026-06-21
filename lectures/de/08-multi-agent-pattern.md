# 08 — Multi-Agenten-Pattern

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../en/08-multi-agent-pattern.md)

## Konzept

Über eine feste sequentielle Pipeline hinaus bietet CrewAI **hierarchische** Orchestrierung: ein Manager-Agent (oder Manager-LLM) entscheidet, welcher Worker-Agent welchen Task übernimmt und in welcher Reihenfolge, statt dass ihr die Sequenz hartcodiert. Das ist das eigentliche "Multi-Agenten"-Pattern — Agenten, deren Zusammenarbeit selbst dynamisch ist, nicht nur eine feste Leitung.

Kompromiss: flexibler, aber weniger vorhersagbar und teurer (der Manager macht zusätzliche LLM-Aufrufe, um zu delegieren).

## In diesem Repo

Aktuell `process=Process.sequential` mit genau zwei Agenten in fester Reihenfolge ([crew.py:50](../../src/research_crew/crew.py#L50)). Um hierarchisch zu werden, braucht CrewAI entweder `manager_llm` oder `manager_agent`:

```python
return Crew(
    agents=self.agents,
    tasks=self.tasks,
    process=Process.hierarchical,
    manager_llm="gemini/gemini-2.5-flash",
    verbose=True,
)
```

## Übung

1. Fügt [crew.py](../../src/research_crew/crew.py) und [config/agents.yaml](../../src/research_crew/config/agents.yaml) einen dritten Agenten hinzu — einen `editor`, dessen Aufgabe es ist, den Report des Analysten auf Ton und Klarheit zu prüfen und zu verfeinern.
2. Fügt in [config/tasks.yaml](../../src/research_crew/config/tasks.yaml) einen entsprechenden `editing_task` mit `context: - analysis_task` hinzu.
3. Stellt `process` auf `Process.hierarchical` um und fügt `manager_llm` hinzu. Entfernt das Feld `agent:` aus jedem Task in `tasks.yaml` — im hierarchischen Modus weist der Manager Tasks dynamisch Agenten zu, statt eine feste Zuordnung zu lesen.
4. Führt es aus und beobachtet die ausführlichen Logs: welchen Agenten wählt der Manager für jeden Task, und entspricht das dem, was ihr von der Rolle jedes Agenten erwarten würdet?

## Zusatzaufgabe

Probiert `manager_agent` statt `manager_llm` — definiert euren eigenen dedizierten Manager-`Agent` mit einer Rolle wie "Editorial Director" und übergebt ihn stattdessen. Vergleicht, ob sich die Delegationsentscheidungen ändern.
