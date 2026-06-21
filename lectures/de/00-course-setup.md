# 00 — Einrichtung des Kurses

🇩🇪 **Deutsch** (diese Seite) · 🇬🇧 [English](../en/00-course-setup.md)

## Konzept

Bevor irgendein Agenten-Code geschrieben wird, braucht jeder eine identische, funktionierende Umgebung. Die zwei häufigsten Zeitfresser in einer Vorlesung sind: Studierende, die an der lokalen Installation hängen bleiben, und Studierende, denen API-Schlüssel fehlen. Beides lösen wir vor Lektion 1.

## In diesem Repo

Dieses Projekt unterstützt zwei Einrichtungswege, dokumentiert im Haupt-[README](../../README.md#getting-started--choose-one-option):

- **Option A: GitHub Codespaces** — keine lokale Installation nötig, läuft im Browser. Der Container führt automatisch `uv sync` aus, gesteuert über [.devcontainer/devcontainer.json](../../.devcontainer/devcontainer.json).
- **Option B: Lokal ausführen** — `uv sync` auf dem eigenen Rechner.

In beiden Fällen werden zwei API-Schlüssel benötigt, bevor überhaupt etwas läuft:
- `GEMINI_API_KEY` — treibt das LLM hinter jedem Agenten an (siehe `MODEL=gemini/gemini-2.5-flash` in `.env.example`)
- `SERPER_API_KEY` — treibt das Web-Such-Tool des Researcher-Agenten an

## Übung

1. Wählt einen Einrichtungsweg (Codespaces oder lokal) und bringt ihn gemäß README zum Laufen.
2. Holt euch eigene kostenlose API-Schlüssel:
   - Gemini: https://ai.google.dev (kostenloses Kontingent)
   - Serper: https://serper.dev (kostenloses Kontingent)
3. Kopiert `.env.example` nach `.env` und tragt eure Schlüssel ein.
4. Führt die Crew einmal aus:
   ```bash
   uv run research_crew
   ```
5. Prüft, dass `output/report.md` erzeugt wurde und einen echten Report enthält (keine Fehlermeldung).

Falls Schritt 5 fehlschlägt, behebt das jetzt — jede spätere Lektion setzt voraus, dass dies funktioniert. Häufige Anfangsprobleme: falscher Name der Umgebungsvariable, Tippfehler im Modellnamen, oder ein erreichtes Rate-Limit im kostenlosen Kontingent (kurz warten und erneut versuchen).

## Zusatzaufgabe

Startet stattdessen die Streamlit-Live-Oberfläche statt der reinen Kommandozeile:
```bash
uv run streamlit run streamlit_app.py
```
Beobachtet, wie die Agent-/Task-/Tool-Ereignisse live einlaufen, während die Crew läuft, statt nur statische Terminal-Ausgabe zu lesen.
