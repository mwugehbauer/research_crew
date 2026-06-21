# 07 — Planning-Pattern

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../en/07-planning-pattern.md)

## Konzept

Statt dass ein Agent Schritt für Schritt improvisiert, erstellt ein **Planner** zunächst einen expliziten Plan — eine Schrittfolge — bevor irgendein Task ausgeführt wird. Das tauscht etwas Latenz/Kosten im Voraus gegen vorhersagbarere, überprüfbare Ausführung: man kann den Plan lesen und einen schlechten Ansatz erkennen, bevor der Agent Tool-Aufrufe und Tokens dafür verbraucht.

## In diesem Repo

CrewAI baut das auf `Crew`-Ebene über zwei Felder ein (`crew.py` nutzt sie noch nicht):

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

Wenn `planning=True` gesetzt ist, führt CrewAI vor Beginn der Ausführung einen internen `AgentPlanner` aus (mit `planning_llm`), der jedem Task-Kontext einen Plan hinzufügt.

## Übung

1. Fügt `planning=True` und `planning_llm="gemini/gemini-2.5-flash"` der `Crew` in [crew.py](../../src/research_crew/crew.py) hinzu.
2. Führt die Crew mit ausführlicher Ausgabe erneut aus und findet den Planning-Schritt in den Logs — er passiert, bevor `research_task` startet. Lest den generierten Plan.
3. Vergleicht zwei Läufe zum selben Thema, einen mit `planning=True` und einen ohne. Verändert der Plan sichtbar *was* der Researcher sucht, oder fügt er nur Overhead ohne Verhaltensänderung hinzu? Schreibt eure Beobachtung auf — es gibt keine einzig richtige Antwort, es geht darum, wirklich hinzusehen.

## Zusatzaufgabe

Planning kostet einen zusätzlichen LLM-Aufruf, bevor überhaupt ein Task läuft. Lohnt sich dieser Overhead für eine Crew mit nur zwei Tasks wie dieser? Argumentiert beide Seiten in ein paar Sätzen, und überlegt dann, ab wann eine Crew genug Tasks/Agenten hat, damit sich Planning erkennbar auszahlt (Tipp: denkt an die Multi-Agenten-Crews aus Lektion 08).
