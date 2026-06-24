# 00 — Course Setup

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](../de/00-course-setup.md)

Before writing any agent code, everyone needs an identical, working environment. The three failure modes that waste the most class time are: students stuck waiting for org/team access, students stuck on local installs, and students missing API keys. We solve all three before exercise 1.

## In this repo

This course runs in a GitHub Organization. Getting access happens once, documented in the main [README's "Getting access" section](../../README.md#getting-access-students): get a GitHub account, submit it via the team sign-up issue, accept your team invite, then your instructor gives your team access to **your own copy of this repo** — that's the one you actually work in from here on, not this exact page's repo.

Once you're in your team's repo, it supports two setup paths, documented in the main [README](../../README.md#getting-started--choose-one-option):

- **Option A: GitHub Codespaces** — zero local install, runs in the browser. The container automatically runs `uv sync` via [.devcontainer/devcontainer.json](../../.devcontainer/devcontainer.json).
- **Option B: Run locally** — `uv sync` on your own machine.

Either way, you need three API keys before anything will run:
- `GROQ_API_KEY` — powers the LLM behind every agent (`MODEL=groq/llama-3.3-70b-versatile`, set automatically by `main.py` if not already present)
- `SERPER_API_KEY` — powers the researcher agent's web search tool
- `GEMINI_API_KEY` — powers embeddings for knowledge/memory features, not the chat LLM (see exercise 03)

**These are set up once per team, not once per student** — see the Task below.

## Task

1. If you haven't already: get a GitHub account, submit your email and username via the team sign-up issue (your instructor reviews it and assigns your team manually — not instant), and accept the team invite once it arrives. Confirm you can see your team's repo before continuing.
2. **As a team, agree on who sets up the API keys** — it only needs to happen once. That person gets the free keys:
   - Groq: https://console.groq.com/keys (free tier)
   - Serper: https://serper.dev (free tier)
   - Gemini: https://ai.google.dev (free tier)
3. That person adds them as **repository secrets** on your team's repo: `Settings → Secrets and variables → Codespaces` → add `GROQ_API_KEY`, `SERPER_API_KEY`, `GEMINI_API_KEY`. Everyone else on the team gets these automatically in any Codespace they open on that repo — nobody else repeats this step. (Running locally instead of Codespaces: copy `.env.example` to `.env` and fill them in there yourself — `.env` isn't shared between teammates the way repository secrets are.)
4. Open your team's repo and run the crew once:
   ```bash
   uv run research_crew
   ```
5. Confirm `output/report.md` was created and contains a real report (not an error).

If a key is missing, `main.py` now fails fast with a clear message naming exactly which key is missing and a link to get one — rather than a deep stack trace from inside `crewai`. If you see that message, fix it and rerun; if step 5 still fails after your keys are set, debug it now — every later exercise assumes this works. Other common first-run issues: a model name typo, hitting a free-tier rate limit (wait a minute and retry), or — if you're on a much older clone of this repo without the `MODEL` default in `main.py` — an `OPENAI_API_KEY is required` error, which means `MODEL` itself never reached the environment (Codespaces secrets bypass `.env.example`'s default value entirely; add `MODEL=groq/llama-3.3-70b-versatile` as a Codespaces secret too, or update `main.py`).

## Stretch goal

Run the Streamlit live-view UI instead of the plain CLI:
```bash
uv run streamlit run streamlit_app.py
```
Watch the agent/task/tool events stream in as the crew runs, instead of reading static terminal output.
