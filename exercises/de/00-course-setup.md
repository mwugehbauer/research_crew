# 00 — Einrichtung des Kurses

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../en/00-course-setup.md)

Bevor irgendein Agenten-Code geschrieben wird, braucht jeder eine identische, funktionierende Umgebung. Die drei häufigsten Zeitfresser sind: Studierende, die auf Org-/Team-Zugang warten, Studierende, die an der lokalen Installation hängen bleiben, und Studierende, denen API-Schlüssel fehlen. Alle drei lösen wir vor Übung 1.

## In diesem Repo

Dieser Kurs läuft in einer GitHub-Organisation. Der Zugang wird einmalig eingerichtet, dokumentiert im Abschnitt ["Zugang erhalten" des Haupt-READMEs](../../README.md#getting-access-students): GitHub-Account holen, über das Team-Anmelde-Issue einreichen, die Team-Einladung annehmen — dann gibt eure Lehrperson eurem Team Zugang zu **eurer eigenen Kopie dieses Repos** — das ist diejenige, in der ihr ab jetzt tatsächlich arbeitet, nicht das Repo dieser Seite hier.

Sobald ihr in eurem Team-Repo seid, unterstützt es zwei Einrichtungswege, dokumentiert im Haupt-[README](../../README.md#getting-started--choose-one-option):

- **Option A: GitHub Codespaces** — keine lokale Installation nötig, läuft im Browser. Der Container führt automatisch `uv sync` aus, gesteuert über [.devcontainer/devcontainer.json](../../.devcontainer/devcontainer.json).
- **Option B: Lokal ausführen** — `uv sync` auf dem eigenen Rechner.

In beiden Fällen werden drei API-Schlüssel benötigt, bevor überhaupt etwas läuft:
- `GROQ_API_KEY` — treibt das LLM hinter jedem Agenten an (`MODEL=groq/llama-3.3-70b-versatile`, von `main.py` automatisch gesetzt, falls noch nicht vorhanden)
- `SERPER_API_KEY` — treibt das Web-Such-Tool des Researcher-Agenten an
- `GEMINI_API_KEY` — treibt Embeddings für Knowledge-/Memory-Funktionen an, nicht das Chat-LLM (siehe Übung 03)

**Diese werden einmal pro Team eingerichtet, nicht einmal pro Studierendem** — siehe die Aufgabe unten.

## Aufgabe

1. Falls noch nicht erledigt: Holt euch einen GitHub-Account, reicht eure E-Mail und euren Benutzernamen über das Team-Anmelde-Issue ein (eure Lehrperson prüft es und weist euer Team manuell zu — nicht sofort), und nehmt die Team-Einladung an, sobald sie ankommt. Prüft, dass ihr euer Team-Repo sehen könnt, bevor ihr weitermacht.
2. **Einigt euch als Team, wer die API-Schlüssel einrichtet** — das muss nur einmal passieren. Diese Person holt sich die kostenlosen Schlüssel:
   - Groq: https://console.groq.com/keys (kostenloses Kontingent)
   - Serper: https://serper.dev (kostenloses Kontingent)
   - Gemini: https://ai.google.dev (kostenloses Kontingent)
3. Diese Person fügt sie als **Repository-Secrets** in eurem Team-Repo hinzu: `Settings → Secrets and variables → Codespaces` → `GROQ_API_KEY`, `SERPER_API_KEY`, `GEMINI_API_KEY` hinzufügen. Alle anderen im Team bekommen diese automatisch in jedem Codespace, den sie auf diesem Repo öffnen — niemand sonst muss diesen Schritt wiederholen. (Falls ihr lokal statt mit Codespaces arbeitet: kopiert `.env.example` nach `.env` und tragt sie dort selbst ein — `.env` wird nicht wie Repository-Secrets automatisch zwischen Teammitgliedern geteilt.)
4. Öffnet euer Team-Repo und führt die Crew einmal aus:
   ```bash
   uv run research_crew
   ```
5. Prüft, dass `output/report.md` erzeugt wurde und einen echten Report enthält (keine Fehlermeldung).

Falls ein Schlüssel fehlt, schlägt `main.py` jetzt sofort mit einer klaren Meldung fehl, die genau benennt, welcher Schlüssel fehlt, plus einem Link, um einen zu bekommen — statt eines tiefen Stack-Traces aus dem Inneren von `crewai`. Behebt das und führt die Crew erneut aus; falls Schritt 5 trotz gesetzter Schlüssel weiter fehlschlägt, behebt das jetzt — jede spätere Übung setzt voraus, dass dies funktioniert. Weitere häufige Anfangsprobleme: ein Tippfehler im Modellnamen, ein erreichtes Rate-Limit im kostenlosen Kontingent (kurz warten und erneut versuchen), oder — bei einem älteren Klon dieses Repos ohne den `MODEL`-Default in `main.py` — ein Fehler "OPENAI_API_KEY is required", der bedeutet, dass `MODEL` selbst nie in der Umgebung angekommen ist (Codespaces-Secrets überspringen den Default-Wert aus `.env.example` komplett; fügt zusätzlich `MODEL=groq/llama-3.3-70b-versatile` als Codespaces-Secret hinzu, oder aktualisiert `main.py`).

## Zusatzaufgabe

Startet stattdessen die Streamlit-Live-Oberfläche statt der reinen Kommandozeile:
```bash
uv run streamlit run streamlit_app.py
```
Beobachtet, wie die Agent-/Task-/Tool-Ereignisse live einlaufen, während die Crew läuft, statt nur statische Terminal-Ausgabe zu lesen.
