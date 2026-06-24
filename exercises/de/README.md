# Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../README.md)

Das sind die praktischen Sprints zu **Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI**. Die Vorlesungstheorie wird über Folien im Kurs vermittelt; diese Reihe ist die praktische Begleitung dazu, nutzt die Demo-Crew dieses Repositorys als durchgängiges Beispiel — und ist zugleich die benotete Team-Aufgabe, kein separates Ding daneben. Jeder Sprint ist etwas, das ihr direkt an **eurem eigenen Anwendungsfall** macht, keine generische Übung, die ihr einmal macht und später für echt wiederholt.

Jeder Sprint hat denselben Aufbau:
- **Hintergrund** — gerade so viel Theorie, um das Konzept einzuordnen, mit Zitat des bahnbrechenden Papers (und der Originalabbildung, wo eine existiert)
- **In diesem Repo** — wo genau das Konzept im Code der Demo-Crew auftaucht, mit Datei-/Zeilenverweisen
- **Aufgabe** — Sprint Planning (GitHub-Issues als User Stories/Epics öffnen) und konkrete Schritte für *eure* Crew, am Ende ein paar gezielte Fragen, die ihr direkt in `DESIGN.md` beantwortet
- **Zusatzaufgabe** (optional) — eine schwerere Anschlussaufgabe für alle, die früher fertig sind

Ihr solltet [Run the crew](../../README.md#getting-started--choose-one-option) in **eurem eigenen Team-Repo** funktionsfähig haben, bevor Sprint 0 beginnt — siehe den Abschnitt ["Zugang erhalten" im Haupt-README](../../README.md#getting-access-students), falls ihr das noch nicht habt.

Lakshmanans *Generative AI Design Patterns* wird als Begleitwerk in Sprint 5 zitiert; Simon (1969) und Brown (2008) begründen die Design-Thinking-Elemente in Sprint 0; alle anderen Zitate sind spezifische arXiv-Papers, aufgeführt pro Sprint.

## Sprints

| # | Titel | Schaltet frei |
| --- | --- | --- |
| [0](00-vision-architecture.md) | Vision & Architektur | Anwendungsfall wählen, Agenten und Tasks entwerfen |
| [1](01-first-mvp.md) | Erster lauffähiger MVP | Eine funktionierende sequentielle (oder parallele) Crew |
| [2](02-tools.md) | Tools | Ein Tool, das euer Anwendungsfall wirklich braucht |
| [3](03-rag.md) | RAG | Verankerte Antworten aus einer echten Knowledge Source *(Zwischenabgabe fällig)* |
| [4](04-dynamic-orchestration.md) | Dynamische Orchestrierung (Hierarchisch) | Ein dritter Agent + manager-delegierter Prozess |
| [5](05-production-safety.md) | Produktionssicherheit & Stabilität | Threat Model, Monitoring-Plan *(Abschlussabgabe fällig)* |

Was bewertet wird und wie, das Abgabepaket, Team-Setup und die Vorlagen (`DESIGN.md`, `TEAM.md`, User Stories, Peer Evaluation), siehe [Überblick zur Aufgabe](assignment-overview.md) (Deutsch / [English](../en/assignment-overview.md)).

## Selbstständig weiterlernen

Der "Hintergrund"-Abschnitt jedes Sprints gibt euch gerade genug, um das Konzept einzuordnen — für alles, was CrewAI selbst über das hinaus kann, was die Demo-Crew in diesem Repo zeigt, geht direkt zur Quelle:
- [CrewAI-Dokumentation](https://docs.crewai.com) — die vollständige Konzept-Referenz (Agents, Tasks, Prozesse, Tools, Memory, Knowledge, Flows) und der [Quickstart](https://docs.crewai.com/en/quickstart)
- [Multi AI Agent Systems with crewAI](https://www.deeplearning.ai/short-courses/multi-ai-agent-systems-with-crewai/) (DeepLearning.AI) — ein kurzer Videokurs, gehalten vom Gründer von CrewAI; kostenlos während der Beta-Phase der DeepLearning.AI-Plattform, bleibt möglicherweise nicht dauerhaft kostenlos

## Für Lehrende

Jeder Sprint verweist auf reale Dateien in `src/research_crew/`. Studierende arbeiten in ihrem eigenen Team-Repo (eines pro Team, aus dieser Vorlage unter eurer Kurs-Organisation erzeugt) — siehe ["Zugang erhalten" im Haupt-README](../../README.md#getting-access-students) für den studierendenseitigen Einschreibe-Ablauf, und den Abschnitt "Für Lehrende" im [Überblick zur Aufgabe](assignment-overview.md#für-lehrende) für die vollständige Org-/Team-/Repo-Einrichtung und den automatisierten Anmelde-Workflow. Musterlösungen sind bewusst nicht enthalten; bewertet Abgaben, indem ihr die gemergten Sprint-Pull-Requests jedes Teams direkt prüft.
