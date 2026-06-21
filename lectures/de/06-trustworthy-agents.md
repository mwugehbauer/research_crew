# 06 — Vertrauenswürdige Agenten bauen

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../en/06-trustworthy-agents.md)

## Konzept

Agenten scheitern auf Arten, wie es einfache Funktionen nicht tun: sie können selbstbewusst falsche Ausgaben produzieren, Anweisungen ignorieren, oder "erfolgreich" sein, während sie Unsinn produzieren. Mechanismen für Vertrauenswürdigkeit fallen grob in zwei Kategorien:
- **Guardrails** — validieren die Ausgabe eines Tasks, *bevor* zum nächsten Schritt übergegangen werden darf, und können optional einen erneuten Versuch erzwingen
- **Evaluation** — bewerten die Ausgabequalität nachträglich, für Monitoring oder Benotung statt für Blockade

## In diesem Repo

CrewAIs `Task` unterstützt einen `guardrail`-Parameter — eine Funktion (oder eine natürlichsprachliche Beschreibung), die die Ausgabe validiert, bevor der nächste Task läuft. Nichts in diesem Repo nutzt das bisher, was es zu einer guten Übung macht: aktuell schreibt `analysis_task` bereitwillig einen Report aus schlechter Eingabe, wenn der `researcher`-Agent ein dünnes oder themenfremdes Ergebnis liefert — ohne jede Prüfung dazwischen.

Für Evaluation liefert `crewai_tools` eine Patronus-Integration (`PatronusEvalTool`, `PatronusLocalEvaluatorTool`, `PatronusPredefinedCriteriaEvalTool` — siehe die Tool-Tabelle im README) zur Bewertung von Agenten-Ausgaben gegen Kriterien.

## Übung

1. Fügt `research_task` in [crew.py](../../src/research_crew/crew.py) ein `guardrail` hinzu, das prüft, ob die Ausgabe nicht verdächtig kurz ist (z. B. weniger als 200 Zeichen), und die Validierung andernfalls scheitern lässt:
   ```python
   def research_quality_guardrail(output):
       if len(output.raw) < 200:
           return (False, "Research output too short — needs more detail")
       return (True, output.raw)

   @task
   def research_task(self) -> Task:
       return Task(
           config=self.tasks_config['research_task'],
           guardrail=research_quality_guardrail,
       )
   ```
2. Erzwingt absichtlich einen Fehlschlag: brecht vorübergehend den `SERPER_API_KEY` (benennt ihn um), sodass der Researcher keine Suchergebnisse zurückbekommt, und prüft, dass das Guardrail die dadurch entstehende dünne Ausgabe abfängt und einen erneuten Versuch auslöst, statt schlechte Daten stillschweigend an den Analysten weiterzugeben.
3. Stellt den Schlüssel wieder her, führt erneut aus, und prüft, dass das Guardrail normale Ausgaben unverändert durchlässt.

## Zusatzaufgabe

Lest über `guardrail_max_retries` bei `Task` (Standardwert 3). Setzt es auf 1 und erklärt, was passiert, wenn das Guardrail weiterhin scheitert — bricht die Crew mit einem Fehler ab, oder macht sie trotzdem weiter? Prüft die Antwort im CrewAI-Quellcode, statt zu raten.
