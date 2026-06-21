# 00 — Course Setup

## Concept

Before writing any agent code, everyone needs an identical, working environment. The two failure modes that waste the most lecture time are: students stuck on local installs, and students missing API keys. We solve both before lecture 1.

## In this repo

This project supports two setup paths, documented in the main [README](../README.md#getting-started--choose-one-option):

- **Option A: GitHub Codespaces** — zero local install, runs in the browser. The container automatically runs `uv sync` via [.devcontainer/devcontainer.json](../.devcontainer/devcontainer.json).
- **Option B: Run locally** — `uv sync` on your own machine.

Either way, you need two API keys before anything will run:
- `GEMINI_API_KEY` — powers the LLM behind every agent (see `MODEL=gemini/gemini-2.5-flash` in `.env.example`)
- `SERPER_API_KEY` — powers the researcher agent's web search tool

## Exercise

1. Pick a setup path (Codespaces or local) and get it running, following the README.
2. Get your own free API keys:
   - Gemini: https://ai.google.dev (free tier)
   - Serper: https://serper.dev (free tier)
3. Copy `.env.example` to `.env` and fill in your keys.
4. Run the crew once:
   ```bash
   uv run research_crew
   ```
5. Confirm `output/report.md` was created and contains a real report (not an error).

If step 5 fails, debug it now — every later lecture assumes this works. Common first-run issues: wrong env var name, model name typo, or hitting a free-tier rate limit (wait a minute and retry).

## Stretch goal

Run the Streamlit live-view UI instead of the plain CLI:
```bash
uv run streamlit run streamlit_app.py
```
Watch the agent/task/tool events stream in as the crew runs, instead of reading static terminal output.
