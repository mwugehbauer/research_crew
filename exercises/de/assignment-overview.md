# Team-Aufgabe — Entwerft eure eigene Crew

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../en/assignment-overview.md)

Dies ist die benotete Aufgabe, die parallel zur Übungsreihe läuft: In Teams entwerft ihr eine CrewAI-Crew zu einem Thema eurer Wahl und baut sie mit wachsender Komplexität aus, während die Übungen neue Fähigkeiten einführen. Das primäre Abgabeprodukt ist in jeder Phase **euer Entwurf plus eure kritische Einschätzung seiner Risiken und Grenzen** — funktionierender Code ist ein optionaler Bonus, nie eine Pflicht.

Siehe [Meilensteine der Aufgabe](assignment-milestones.md) dafür, was in welcher Phase zu bauen ist, [Vorlagen für die Aufgabe](assignment-templates.md) für die Dokumente, die ihr ausfüllt, und den [Sprint-Plan](assignment-sprint-plan.md), falls ihr das als echte Scrum-Sprints mit Sprint Planning/Review/Retrospektive durchführen wollt.

## So funktioniert es: Sprints entlang der Übungen

Behandelt jede Übung als Sprint-Grenze. Jeder Sprint schaltet eine neue Fähigkeit ("Epic") für euren Crew-Entwurf frei — ihr entwerft nicht jedes Mal neu, sondern erweitert, was schon da ist.

| Übung(en) | Schaltet frei | Meilenstein |
| --- | --- | --- |
| [01](01-agentic-frameworks.md) | Agenten, Tasks, sequentieller Prozess | **M0: Baseline** |
| [02](02-tool-use.md) | Tool-Nutzung | **M1: Tools** |
| [03](03-agentic-rag.md) | Knowledge Sources / RAG | **M2: RAG** *(Zwischenabgabe hier fällig)* |
| [04](04-multi-agent-pattern.md) | Multi-Agenten-/hierarchischer Prozess | **M3: Multi-Agent** |
| [05](05-production.md) + [06](06-securing-agents.md) | Produktions-Aspekte, Security-Threat-Modeling | **Abschluss: Produktion und Sicherheit** |

Zwei Abgaben: eine **Zwischenabgabe** bei M2 (formativ, geringeres Gewicht — fängt schwache Grundlagen früh ab) und eine **Abschlussabgabe** nach der letzten Übung (der vollständige Entwurf plus eine Retrospektive darüber, wie sich euer Denken verändert hat).

## Team-Setup: Repos und Accounts

Dieser Kurs läuft in einer GitHub-Organisation, mit **einem privaten Repository pro Team — nicht eines pro Studierendem.** Ihr legt dieses Repo nicht selbst an; eure Lehrperson hat es bereits aus der Kursvorlage erzeugt, eines pro Team, und gibt eurem Team Zugang dazu, sobald ihr eingeschrieben seid. Siehe den Abschnitt ["Zugang erhalten" im Haupt-README](../../README.md#getting-access-students) für die Einschreibe-Schritte (GitHub-Account → Team-Anmelde-Issue → Einladung annehmen).

**Jedes Teammitglied braucht trotzdem einen eigenen GitHub-Account**, dem Team in der Organisation hinzugefügt (nicht nur direkt einem Repo). Zwei Gründe: Eure einzelnen Commits sind die Grundlage, anhand der der individuelle Beitrag im Team bewertet wird, und eine echte Commit-Historie unter eurem eigenen Account ist über diesen Kurs hinaus etwas wert.

### Zusammenarbeiten ohne Git-Erfahrung

Für die tägliche Teamarbeit braucht ihr keine Branches oder Pull Requests — ein einfacher Ablauf reicht:

1. Bearbeitet eine Datei wie gewohnt (in eurem Codespace).
2. Öffnet das **Source-Control-Panel** (das Verzweigungs-Icon in der Seitenleiste).
3. Schreibt eine kurze Commit-Nachricht, klickt auf **✓ Commit**.
4. Klickt auf **Sync Changes** — das holt in einem Schritt die Änderungen eurer Teammitglieder und schiebt eure eigenen hoch.

Kein Terminal, keine `git add`/`commit`/`push`-Befehle. Alle committen direkt auf `main`.

Um zu vermeiden, dass zwei Personen dieselbe Datei gleichzeitig bearbeiten, **teilt Dateien zwischen Teammitgliedern auf**, wo es geht — z. B. verwaltet eine Person `agents.yaml`, eine andere `tasks.yaml`. `DESIGN.md` ist eine gemeinsame Datei, zu der alle beitragen — wechselt euch dabei ab, oder committet und synct alle paar Minuten, statt lange parallel in derselben Datei zu arbeiten. Falls trotzdem ein Konflikt auftritt, zeigt VS Code eine Merge-Ansicht mit anklickbaren Buttons ("Accept Current / Incoming / Both") — bittet eure Lehrperson einmal um eine kurze Live-Demo davon, damit es niemanden mitten in einer Deadline überrascht.

Für schnelle Änderungen (z. B. einen `RISK_LOG.md`-Eintrag) könnt ihr Codespaces ganz überspringen: Öffnet die Datei auf github.com, klickt auf das Stift-Icon, bearbeitet sie im Browser und klickt unten auf **"Commit changes"**.

## Abgabepaket

Bei jeder Meilenstein-Deadline ist eure Abgabe der Zustand des `main`-Branchs eures Team-Repos:

| Artefakt | Wo | Was es zeigt |
| --- | --- | --- |
| Lauffähige Crew-Konfiguration | `src/research_crew/config/agents.yaml` + `tasks.yaml` (+ `crew.py`, sobald Tools/RAG/Prozess sich ändern) | Die buchstäbliche, lauffähige Version eures Entwurfs |
| Design-Dokument | `DESIGN.md` — Architektur (Agenten/Tasks/Tools/RAG), Risiken, Grenzen, Sicherheit, Produktions-Aspekte, Design-Historie | Eure vollständige, kritisch geprüfte Entwurfsbegründung, in einem sich entwickelnden Bericht |
| Backlog | GitHub Issues (nach Epic gelabelt) + ein Projects-Board | Eure User Stories und euer Fortschritt — lebt auf GitHub, nichts zu exportieren |
| Team-Notizen | `TEAM.md` | Mitglieder und wer was beigetragen hat |
| Optionaler Bonus | ein funktionierendes `crew.py` + ein erfolgreiches `uv run research_crew` | Nur Zusatzpunkte — nie Pflicht |

Die Abgabe ist einfach **der Zustand des `main`-Branchs eures Team-Repos zur Deadline** — es gibt keinen Pull Request zu öffnen. Teilt eure Repo-URL einmal, am Anfang; eure Lehrperson prüft eure Commit-Historie zu jeder Deadline in genau diesem Repo (und kann dafür einen bestimmten Commit taggen).

## Bewertung

Die Entwurfsdokumente (`agents.yaml`/`tasks.yaml` + `DESIGN.md` + Backlog) tragen den weit überwiegenden Teil der Note. Funktionierender Code gibt Bonuspunkte oben drauf, ersetzt aber nie eine dünne oder fehlende Risikoanalyse. Siehe [Meilensteine der Aufgabe](assignment-milestones.md) für die konkreten, pro Phase bewerteten Risikoanalyse-Fragen.

## Agile Praxis: Backlog und User Stories

Führt euren Entwurfsprozess wie ein echtes Produkt-Backlog:
- Die neue Fähigkeit jedes Meilensteins ist ein **Epic**. Brecht es in 2–4 **User Stories** herunter: *"Als [Stakeholder des Crew-Ergebnisses] möchte ich [Fähigkeit], damit [Nutzen]."*
- Schreibt **Akzeptanzkriterien** für jede Story als testbare Bedingungen — diese sind zugleich ein Entwurf für das `expected_output`-Feld des Tasks, sobald ihr beim YAML angelangt seid, was an sich schon eine nützliche Beobachtung ist.
- Fügt jedem Epic "Risiko identifiziert und dokumentiert" zur Definition of Done hinzu, damit Risikoanalyse eine Gewohnheit wird, kein einmaliger Aufsatz.
- Ist euer Team größer als zwei, rotiert die Facilitator-Rolle jeden Sprint.

Vorlagen dafür findet ihr unter [Vorlagen für die Aufgabe](assignment-templates.md); eine vollständige Sprint-für-Sprint-Aufschlüsselung (Planning-Checkliste, Definition of Done, Review, Retrospektive) im [Sprint-Plan](assignment-sprint-plan.md).

## Für Lehrende

Das ist die einmalige Einrichtung hinter allem oben. GitHub Classroom nimmt seit Mai 2026 keine neuen Anmeldungen mehr an — das hier ersetzt es durch reine GitHub-Organisation-Funktionen, der Free-Plan deckt alles ab (unbegrenzte Mitglieder, unbegrenzte private Repos).

### 1. Organisation und Teams anlegen

Legt eine kostenlose Organisation an, dann **Settings → Teams → New team** einmal pro Projektgruppe (z. B. `team-a`, `team-b`, ...). Optional könnt ihr alle unter einem Parent-Team verschachteln (z. B. `students`), falls ihr ein gemeinsames Ressourcen-Repo wollt, das automatisch für alle sichtbar ist — Child-Teams erben alles, was das Parent-Team sehen kann.

### 2. Dieses Repo als Vorlage markieren, dann ein Repo pro Team erzeugen

Dieses Repo: **Settings → "Template repository" anhaken**. Dann pro Team:
```bash
gh repo create <org>/<team-slug>-crew --template <org>/<dieses-repo> --private
gh api repos/<org>/<team-slug>-crew/teams/<team-slug> -X PUT -f permission=admin
```
**Admin** (nicht nur Write) ist hier wichtig — das Verwalten der Secrets eines Repos braucht Admin, und ihr wollt, dass jedes Team seine API-Schlüssel selbst einrichten kann, ohne dass ihr dazwischen müsst.

### 3. Codespaces für die Organisation aktivieren

**Org Settings → Codespaces → General** → für alle Repositories aktivieren (oder gezielt die Team-Repos auswählen). Im Free-Plan rechnet Codespaces-Nutzung gegen das persönliche kostenlose Kontingent jedes Studierenden, nicht gegen die Organisation — kein Spending-Limit einzurichten.

### 4. Automatische Team-Einschreibung einrichten

Studierende reichen ihren GitHub-Benutzernamen über ein [Team-Anmelde-Issue](../../.github/ISSUE_TEMPLATE/team-signup.yml) auf diesem Repo ein, und ein [Workflow](../../.github/workflows/add-to-team.yml) fügt sie automatisch ihrem Team hinzu. Dafür wird ein Secret benötigt, das der Standard-`GITHUB_TOKEN` nicht bereitstellen kann, da Team-Mitgliedschaft eine Organisations-Berechtigung ist:

1. Erstellt ein Personal Access Token mit **Organization → Members: Read and write** und **Repository → Issues: Read and write** (fine-grained), oder `admin:org` + `repo` (classic).
2. Fügt es als Secret namens `ORG_ADMIN_TOKEN` hinzu — entweder auf diesem Repo selbst (**Settings → Secrets and variables → Actions**) oder auf Organisationsebene, beschränkt auf dieses Repo (**Org Settings → Secrets and variables → Actions**).
3. Das war's — der Workflow übernimmt Parsen, Hinzufügen, Antworten und Schließen des Issues automatisch. Fehler (vertippter Benutzername, falscher Team-Slug) werden als klarer Kommentar auf dem Issue zurückgemeldet, statt stillschweigend zu scheitern.

### 5. Laufend: Abgaben prüfen

Prüft die Commit-Historie jedes Teams auf `main` zu jeder Deadline — taggt selbst einen bestimmten Commit (Releases → "Create a new release"), wenn ihr einen unveränderlichen Stand für die Bewertung wollt. Musterlösungen sind bewusst nicht enthalten, wie im Rest dieser Reihe.
