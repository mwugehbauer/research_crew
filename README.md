# Generative & Agentic AI — Hands-On Exercises

*Companion repository for the exercise sessions of* **Aktuelle Fallstudien der Digitalökonomie und der Künstlichen Intelligenz: Generative und Agentische KI**.

Lecture theory is delivered via slides in class. This repository is the hands-on practice companion: a small, working multi-agent AI system built with [CrewAI](https://crewai.com) that you'll read, run, and extend across the exercise sessions — plus a graded team assignment where you design your own agentic AI architecture for a use case of your choice.

## Goal

The goal of these exercises is to turn the architectural concepts from the lecture — agents, tasks, tools, RAG, multi-agent orchestration, trust, production, security — from slides into things you've actually read, run, and modified in working code. By the end, you'll be able to **design**, and optionally **implement**, your own agentic AI architecture for a real use case, using CrewAI as the concrete framework.

## Intro to CrewAI

[CrewAI](https://docs.crewai.com) is a Python framework for orchestrating multiple LLM-powered agents that collaborate on a shared set of tasks, instead of one model trying to do everything in a single call. Four abstractions do all the work:

- **Agent** — a `role`, `goal`, `backstory`, an LLM, and optionally `tools`
- **Task** — a `description`, an `expected_output`, and which agent is assigned to it
- **Crew** — the collection of agents + tasks + a `process` for running them
- **Process** — the orchestration strategy: `sequential` (fixed pipeline) or `hierarchical` (a manager agent delegates dynamically)

CrewAI's signature choice — covered in depth in [exercise 01](exercises/en/01-agentic-frameworks.md) — is that `role`/`goal`/`backstory`/task definitions live in **YAML config**, not Python, so you can usually change *what* a crew does without touching the orchestration code at all.

## The template code

This repo's working crew (`researcher` → `analyst`, sequential) is the running example for every exercise:

| File | What it is |
| --- | --- |
| [src/research_crew/crew.py](src/research_crew/crew.py) | Defines the agents, tasks, and the `Crew` itself — short on purpose |
| [src/research_crew/config/agents.yaml](src/research_crew/config/agents.yaml) | Each agent's `role`/`goal`/`backstory` |
| [src/research_crew/config/tasks.yaml](src/research_crew/config/tasks.yaml) | Each task's `description`/`expected_output`/agent assignment |
| [src/research_crew/main.py](src/research_crew/main.py) | Entry point — sets the `topic` input and kicks off the crew |
| [src/research_crew/tools/custom_tool.py](src/research_crew/tools/custom_tool.py) | An unwired template for writing your own tool (exercise 02) |
| [src/research_crew/knowledge_source_example.py](src/research_crew/knowledge_source_example.py) | A working, unwired `build_knowledge_sources()` helper for RAG (exercise 03) |

## Use cases to pick from

For the team assignment (see below), you design your own crew for a use case of your choice — including your own agent roles and task flow, not the starter repo's `researcher`/`analyst` relabeled with a new topic. You're reusing the same CrewAI mechanics already in this repo (`Agent`/`Task`/`Crew`/`Process`, the same `agents.yaml`/`tasks.yaml` files) — never rewriting code from scratch, just designing new content for it. Pick one, or propose your own; the role splits below are starting points, not specs — push back on them if your topic calls for something different:

| # | Use case | Example topic & suggested role split | Natural tool to add | Natural RAG source to add |
| --- | --- | --- | --- | --- |
| 1 | Competitive landscape analysis | "Competitive landscape for [industry]"<br>*Market Scout → Positioning Strategist* | Web search / scraping | Market-positioning brief (PDF) |
| 2 | Regulatory impact briefing | "EU AI Act impact on SaaS startups"<br>*Policy Tracker → Compliance Strategist* | Web search | The regulation text itself |
| 3 | Academic literature review | "Recent advances in [CS/AI subtopic]"<br>*Literature Scout → Synthesis Writer* | `ArxivPaperTool` | A seminal paper's PDF |
| 4 | Job market & skills trend report | "In-demand skills for [tech field]"<br>*Labor Market Researcher → Workforce Strategist* | Web search / job search tool | A skills-framework doc |
| 5 | Startup due-diligence memo | "Due diligence on [startup]"<br>*Diligence Researcher → Investment Analyst* | Web search | The startup's pitch deck (PDF) |
| 6 | Personalized travel planner | "Travel plan for [destination]"<br>*Destination Scout → Itinerary Planner* | Web search | Reuse `knowledge/user_preference.txt` |
| 7 | Product sentiment synthesis | "Customer sentiment on [product category]"<br>*Voice-of-Customer Researcher → Product Strategist* | Web search / scraping | The product's FAQ/support docs |
| 8 | ESG/sustainability risk briefing | "ESG risks for [company/sector]"<br>*ESG Researcher → Risk Assessor* | Web search | The company's sustainability report |
| 9 | Personal finance topic explainer | "ETFs vs. individual stocks"<br>*Finance Researcher → Plain-Language Educator* | Web search | A fund prospectus or glossary |
| 10 | News digest on an ongoing story | "Weekly digest on [news topic]"<br>*News Tracker → Digest Editor* | Web search / news search tool | A backgrounder doc |

Full detail (why each is low-friction on the code side despite the new role design, and exactly what changes at each milestone) is in [exercises/en/assignment-milestones.md](exercises/en/assignment-milestones.md).

## Getting access (students)

This course runs in a GitHub Organization, not on this repo directly. Everything below happens once, before your first exercise:

1. **Get a GitHub account** if you don't already have one — free, just an email signup.
2. **Submit your details**: open a [team sign-up issue](https://github.com/hsk-ms-elective-agentic-ai/Ms_Elective_KI/issues/new?template=team-signup.yml) with your email and your GitHub username. You don't pick your team yourself — your instructor reviews the issue and assigns your team manually (not instant), which triggers a GitHub Action that adds you automatically.
3. **Accept the invite** — check your GitHub notifications/email and accept the team invitation. You have no access until you do this step.
4. Once you're on your team, your instructor gives your team access to **your own copy of this repo** (created from this template, one per team) — that's the repo you'll actually work in for every exercise and the team assignment, not this one.

Everything from "Getting started" onward in this README applies to **your team's repo**, once you have access to it.

## Getting started — choose one option

There are two independent ways to get this project running. Pick **one**. (If you're a student: do this in your team's own repo, not here.)

- **Option A — GitHub Codespaces:** run entirely in the browser, nothing installed on your machine.
- **Option B — Run locally:** clone the repo and run it with Python/uv on your own computer.

Both options end up running the exact same code; only the setup step differs. Everything below "Run the crew" applies regardless of which option you picked.

### Option A: GitHub Codespaces (no local install)

No local install needed. Open your team's repo on github.com → **Code → Create codespace on master**.

The container automatically installs `uv` and runs `uv sync`.

**API keys are set up once per team, not per student**: at least one team member gets the free keys and adds them as **repository secrets** on your team's repo (`Settings → Secrets and variables → Codespaces`) — `GROQ_API_KEY`, `SERPER_API_KEY`, `GEMINI_API_KEY`. Once set, every teammate gets them automatically in any Codespace opened on that repo — nobody else needs to do this step. See [Assignment Overview](exercises/en/assignment-overview.md#team-setup-repos-and-accounts) for exactly how this works and the rate-limit tradeoff to know about.

<details>
<summary>Alternative: local <code>.env</code> file inside the codespace (only if you can't use Codespaces secrets)</summary>

Copy `.env.example` to `.env` inside the codespace and fill in your keys — **edit `.env`, not `.env.example`** (the latter is the committed template and stays empty; real keys belong only in `.env`, which is gitignored).
</details>

Once that's done, skip ahead to [Run the crew](#run-the-crew) below.

### Option B: Run locally

Ensure you have Python >=3.10 <3.14 installed on your system. This project uses [UV](https://docs.astral.sh/uv/) for dependency management and package handling, offering a seamless setup and execution experience.

First, if you haven't already, install uv:

```bash
pip install uv
```

Clone the repo, then from its root install the dependencies:

```bash
uv sync
```

Copy `.env.example` to `.env` and fill in `GROQ_API_KEY`, `SERPER_API_KEY`, and `GEMINI_API_KEY` — ask your team for the keys they already set up as repository secrets (see Option A) rather than signing up again locally, unless you specifically want your own.

Once that's done, continue with [Run the crew](#run-the-crew) below.

### Customizing

**Make sure your `.env` has the right API keys for whichever LLM/tools you use**

- Modify `src/research_crew/config/agents.yaml` to define your agents
- Modify `src/research_crew/config/tasks.yaml` to define your tasks
- Modify `src/research_crew/crew.py` to add your own logic, tools and specific args
- Modify `src/research_crew/main.py` to add custom inputs for your agents and tasks

## Run the crew

This applies whether you set up via Codespaces or locally. From the project root:

```bash
uv run research_crew
```

This initializes the research_crew Crew, assembling the agents and assigning them tasks as defined in your configuration, and saves the report to `output/report.md`.

## Live demo UI (Streamlit)

For a classroom-friendly view of the agents working, run the Streamlit app instead of the plain CLI. It shows each agent/task/tool event live in the browser, then renders the final report.

```bash
uv run streamlit run streamlit_app.py
```

Locally this opens at `http://localhost:8501`. In a Codespace, port `8501` is auto-forwarded and a preview tab opens automatically (configured in `.devcontainer/devcontainer.json`).

## Exercise sessions

7 exercise sessions ([English](exercises/README.md) / [Deutsch](exercises/de/README.md)) cover agent concepts, tools, RAG, multi-agent patterns, production, and security — scoped to what's actually demonstrated in this repo's code. Each one starts directly with the practical work, weaving in just enough background from the relevant paper (a short citation and, where one exists, its original figure) to place the concept, then goes straight into where it shows up in this repo's code, a hands-on task, and an optional stretch goal — a hands-on companion to the lecture, not a second lecture.

## Team assignment

Alongside the exercise sessions, teams design their own crew for a use case of their choice (see the table above), growing it in complexity milestone-by-milestone as new sessions unlock new capabilities — a critical risk/constraint analysis is the main graded deliverable, working code is an optional bonus. Plan the work itself using GitHub Issues as epics/user stories, organized into sprints — see the [Sprint Plan](exercises/en/assignment-sprint-plan.md). Start at [exercises/en/assignment-overview.md](exercises/en/assignment-overview.md) (English / [Deutsch](exercises/de/assignment-overview.md)).

## Adding more tools or RAG (for students)

`crewai_tools` ships ~90 built-in tools beyond `SerperDevTool`. The setup that matters most is whether a tool calls an external API directly (just needs a key) or does **local embedding-based search** (needs an embedder pointed at Gemini, same as below) — that split is called out per category.

| Category | Needs embedder config? | Tools |
| --- | --- | --- |
| Web search | No — just an API key | `SerperDevTool`, `TavilySearchTool`, `BraveSearchTool`, `EXASearchTool`, `SerpApiGoogleSearchTool`, `SerpApiGoogleShoppingTool`, `SerplyWebSearchTool`, `SerplyNewsSearchTool`, `SerplyJobSearchTool`, `SerplyScholarSearchTool`, `LinkupSearchTool`, `ParallelSearchTool`, `ArxivPaperTool`, `FirecrawlSearchTool` |
| Web scraping & browser automation | No — just an API key | `ScrapeWebsiteTool`, `ScrapeElementFromWebsiteTool`, `SerperScrapeWebsiteTool`, `SerplyWebpageToMarkdownTool`, `FirecrawlScrapeWebsiteTool`, `FirecrawlCrawlWebsiteTool`, `JinaScrapeWebsiteTool`, `ScrapflyScrapeWebsiteTool`, `ScrapegraphScrapeTool`, `SeleniumScrapingTool`, `SpiderTool`, `BrowserbaseLoadTool`, `HyperbrowserLoadTool`, `StagehandTool`, `MultiOnTool`, `TavilyExtractorTool`, `BrightDataSearchTool`, `BrightDataWebUnlockerTool`, `BrightDataDatasetTool`, `OxylabsAmazonProductScraperTool`, `OxylabsAmazonSearchScraperTool`, `OxylabsGoogleSearchScraperTool`, `OxylabsUniversalScraperTool` |
| Local RAG / semantic content search | **Yes** — defaults to OpenAI embeddings | `RagTool` (base class), `WebsiteSearchTool`, `PDFSearchTool`, `CSVSearchTool`, `DOCXSearchTool`, `JSONSearchTool`, `MDXSearchTool`, `TXTSearchTool`, `XMLSearchTool`, `CodeDocsSearchTool`, `GithubSearchTool`, `YoutubeVideoSearchTool`, `YoutubeChannelSearchTool`, `DirectorySearchTool` |
| Vector database connectors | Bring your own embeddings/index | `QdrantVectorSearchTool`, `WeaviateVectorSearchTool`, `MongoDBVectorSearchTool`, `CouchbaseFTSVectorSearchTool` |
| Databases & structured data | No | `MySQLSearchTool`, `SnowflakeSearchTool`, `SingleStoreSearchTool`, `DatabricksQueryTool`, `NL2SQLTool` |
| File & storage I/O | No | `FileReadTool`, `FileWriterTool`, `FileCompressorTool`, `DirectoryReadTool`, `S3ReaderTool`, `S3WriterTool` |
| Code execution | No | `CodeInterpreterTool` |
| Vision, image & OCR | No | `DallETool`, `VisionTool`, `OCRTool` |
| Evaluation & quality | No | `PatronusEvalTool`, `PatronusLocalEvaluatorTool`, `PatronusPredefinedCriteriaEvalTool` |
| Platform & automation integrations | Varies by platform | `ZapierActionTool`, `ComposioTool`, `ApifyActorsTool`, `EnterpriseActionTool`, `MergeAgentHandlerTool`, `GenerateCrewaiAutomationTool`, `InvokeCrewAIAutomationTool`, `BedrockInvokeAgentTool`, `BedrockKBRetrieverTool`, `AIMindTool`, `LlamaIndexTool`, `ContextualAICreateAgentTool`, `ContextualAIParseTool`, `ContextualAIQueryTool`, `ContextualAIRerankTool` |

For any tool marked "Needs embedder config", point it at Gemini the same way (otherwise it fails with a missing `OPENAI_API_KEY` error, even though the crew's chat LLM is Groq):

```python
WebsiteSearchTool(config={
    "embedding_model": {
        "provider": "google-generativeai",
        "config": {"api_key": os.getenv("GEMINI_API_KEY"), "model_name": "gemini-embedding-001"},
    },
})
```

This crew's `embedder` (see `crew.py`) is already configured the same way at the `Crew` level, so adding a `knowledge_sources=[...]` list there (e.g. a `TextFileKnowledgeSource` pointing at `knowledge/user_preference.txt`) will embed via Gemini automatically — that wiring is left as a hands-on task in exercise 03.

## Support

For support, questions, or feedback regarding CrewAI itself (not the exercises):
- Visit the [CrewAI documentation](https://docs.crewai.com)
- Reach out via the [CrewAI GitHub repository](https://github.com/crewAIInc/crewAI)
- [Join the CrewAI Discord](https://discord.com/invite/X4JWnZnxPb)
