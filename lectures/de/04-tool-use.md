# 04 — Tool-Nutzung

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../en/04-tool-use.md)

## Konzept

Tools verwandeln ein LLM von "erzeugt plausiblen Text" in "kann tatsächlich etwas tun": das Web durchsuchen, eine Datenbank abfragen, eine interne API aufrufen, Code ausführen. Der Agent entscheidet *wann* und *mit welchen Argumenten* er ein Tool aufruft — ihr müsst das Tool nur klar genug beschreiben, damit das LLM es korrekt einsetzen kann.

Jedes CrewAI-Tool braucht:
- einen **Namen** und eine **Beschreibung** (das liest der Agent, um zu entscheiden, ob/wie er es einsetzt — vage Beschreibungen führen zu Fehlgebrauch)
- ein **Eingabeschema** (ein Pydantic-Modell, das die Argumente beschreibt)
- eine `_run()`-Methode mit der eigentlichen Implementierung

## In diesem Repo

[src/research_crew/tools/custom_tool.py](../../src/research_crew/tools/custom_tool.py) ist eine Vorlage, noch nicht in die Crew eingebunden:

```python
class MyCustomTool(BaseTool):
    name: str = "Name of my tool"
    description: str = (
        "Clear description for what this tool is useful for, your agent will need this information to use it."
    )
    args_schema: Type[BaseModel] = MyCustomToolInput

    def _run(self, argument: str) -> str:
        return "this is an example of a tool output, ignore it and move along."
```

Vergleicht es mit dem bereits genutzten Tool, [crew.py:20](../../src/research_crew/crew.py#L20): `SerperDevTool()` — ein vollständig fertiges Tool aus `crewai_tools`, das keine Implementierung benötigt, nur einen API-Schlüssel (`SERPER_API_KEY`).

Die [Tool-Kategorientabelle](../../README.md#adding-more-tools-or-rag-for-students) im README listet ~90 fertige Tools auf, aufgeteilt danach, ob sie nur einen API-Schlüssel brauchen (die meisten Such-/Scraping-Tools) oder lokale Embeddings (RAG-artige Tools, Thema von Lektion 05).

## Übung

1. Implementiert `MyCustomTool` wirklich. Vorschläge: ein einfacher Taschenrechner (ohne `eval` — aus Sicherheitsgründen manuell parsen und berechnen), ein Tool, das das aktuelle Datum/die Uhrzeit liefert, oder ein Tool, das Wörter in einem String zählt.
2. Schreibt einen klaren `name` und eine klare `description` — schlechte führen dazu, dass der Agent das Tool nie aufruft oder mit falschen Argumenten aufruft. Testet sowohl eine vage als auch eine präzise Beschreibung; vergleicht, ob der Agent das Tool nutzt.
3. Fügt euer Tool zu einem der Agenten in [crew.py](../../src/research_crew/crew.py) hinzu (`tools=[SerperDevTool(), MyCustomTool()]`) und formuliert eine Task-Beschreibung, die den Agenten dazu bringen sollte, es nutzen zu wollen.

## Zusatzaufgabe

Tauscht `SerperDevTool` gegen eines der anderen fertigen Such-Tools aus der README-Tabelle (z. B. `TavilySearchTool`) und bringt es mit einem eigenen kostenlosen API-Schlüssel dieses Anbieters zum Laufen.
