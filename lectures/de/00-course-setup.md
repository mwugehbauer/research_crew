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
3. Tragt eure Schlüssel ein: Auf Codespaces fügt sie als **Codespaces-Secrets** unter [github.com/settings/codespaces](https://github.com/settings/codespaces) hinzu, *bevor* ihr euren Codespace öffnet — das ist der empfohlene Weg, da ihr dadurch nie eine Datei mit echten Schlüsseln berührt. Lokal kopiert `.env.example` nach `.env` und tragt sie dort ein (nicht in `.env.example` selbst — diese Datei ist committed und muss leer bleiben).
4. Führt die Crew einmal aus:
   ```bash
   uv run research_crew
   ```
5. Prüft, dass `output/report.md` erzeugt wurde und einen echten Report enthält (keine Fehlermeldung).

Falls ein Schlüssel fehlt, schlägt `main.py` jetzt sofort mit einer klaren Meldung fehl, die genau benennt, welcher Schlüssel fehlt, plus einem Link, um einen zu bekommen — statt eines tiefen Stack-Traces aus dem Inneren von `crewai`. Behebt das und führt die Crew erneut aus; falls Schritt 5 trotz gesetzter Schlüssel weiter fehlschlägt, behebt das jetzt — jede spätere Lektion setzt voraus, dass dies funktioniert. Weitere häufige Anfangsprobleme: Tippfehler im Modellnamen, oder ein erreichtes Rate-Limit im kostenlosen Kontingent (kurz warten und erneut versuchen).

## Zusatzaufgabe

Startet stattdessen die Streamlit-Live-Oberfläche statt der reinen Kommandozeile:
```bash
uv run streamlit run streamlit_app.py
```
Beobachtet, wie die Agent-/Task-/Tool-Ereignisse live einlaufen, während die Crew läuft, statt nur statische Terminal-Ausgabe zu lesen.
