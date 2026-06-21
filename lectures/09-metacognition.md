# 09 — Metacognition

## Concept

Metacognition means an agent (or the system around it) reflects on its own output and improves it, rather than emitting a first draft as final. Two common implementations:
- A **reviewer agent** that critiques another agent's output and sends it back for revision
- A **self-critique loop** where the same agent re-reads and improves its own work

This is different from a guardrail (lecture 06): a guardrail blocks/retries based on a pass/fail check, while metacognition is about *improving quality* through reflection, not gatekeeping.

## In this repo

Nothing here does this yet — `analysis_task`'s output goes straight to `output_file='output/report.md'` with no review step ([config/tasks.yaml](../src/research_crew/config/tasks.yaml)). This is the gap for this exercise.

## Exercise

1. Add a third task, `review_task`, assigned to a new `reviewer` agent (or reuse `analyst`) whose job is to critique the report: does it fully address the topic, is anything vague or unsupported, is the executive summary actually executive-summary-length?
2. Give `review_task` `context: - analysis_task` so it receives the report.
3. Decide on a structure for the critique output: either (a) the reviewer rewrites the report directly with fixes applied, or (b) the reviewer produces a list of issues that a human (you) reads and decides whether to act on. Implement one.
4. Run the full crew and read the reviewer's critique. Was it substantive (caught a real gap) or generic ("looks good!")? If generic, revise the reviewer's `goal`/`backstory` in `agents.yaml` to demand specificity, and compare.

## Stretch goal

Make it an actual loop instead of a one-pass review: if the reviewer's critique contains specific issues, feed those back into a guardrail on `analysis_task` (lecture 06) so the analyst must address them before the crew considers the task done. This combines metacognition (the critique) with guardrails (enforcement) — notice how the two patterns compose.
