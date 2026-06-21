# 04 — Tool Use

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](../de/04-tool-use.md)

## Concept

Tools turn an LLM from "generates plausible text" into "can actually do things": search the web, query a database, call an internal API, run code. The agent decides *when* and *with what arguments* to call a tool — you just need to describe the tool clearly enough that the LLM can use it correctly.

Every CrewAI tool needs:
- a **name** and **description** (this is what the agent reads to decide whether/how to use it — vague descriptions cause misuse)
- an **input schema** (a Pydantic model describing the arguments)
- a `_run()` method with the actual implementation

## In this repo

[src/research_crew/tools/custom_tool.py](../../src/research_crew/tools/custom_tool.py) is a template, not wired into the crew yet:

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

Compare it to the tool already in use, [crew.py:20](../../src/research_crew/crew.py#L20): `SerperDevTool()` — a fully pre-built tool from `crewai_tools`, requiring zero implementation, just an API key (`SERPER_API_KEY`).

The README's [tool category table](../../README.md#adding-more-tools-or-rag-for-students) lists ~90 pre-built tools split by whether they need just an API key (most search/scraping tools) or local embeddings (RAG-style tools, covered in lecture 05).

## Exercise

1. Implement `MyCustomTool` for real. Suggestions: a simple calculator (`eval`-free — parse and compute manually for safety), a tool that returns the current date/time, or a tool that counts words in a string.
2. Write a clear `name` and `description` — bad ones cause the agent to never call the tool, or call it with wrong arguments. Test both a vague description and a precise one; compare whether the agent uses the tool.
3. Add your tool to one of the agents in [crew.py](../../src/research_crew/crew.py) (`tools=[SerperDevTool(), MyCustomTool()]`) and craft a task description that should make the agent want to use it.

## Stretch goal

Swap `SerperDevTool` for one of the other pre-built search tools in the README's table (e.g. `TavilySearchTool`) and get it running with your own free API key from that provider.
