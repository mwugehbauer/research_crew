# Team Assignment — Design Your Own Crew

🇬🇧 **English** (this page) · 🇩🇪 [Deutsch](../de/assignment-overview.md)

This is the graded assignment that runs alongside the exercise series: in teams, you design a CrewAI crew for a topic of your choice, growing it in complexity as the exercises introduce new capabilities. The primary deliverable at every stage is **your design plus your critical assessment of its risks and constraints** — working code is an optional bonus, never a requirement.

See [Assignment Milestones](assignment-milestones.md) for what to build at each stage, [Assignment Templates](assignment-templates.md) for the documents you'll fill in, and the [Sprint Plan](assignment-sprint-plan.md) if you want to run this as actual Scrum sprints with sprint planning/review/retrospective built in.

## How this works: sprints tied to exercises

Treat each exercise as a sprint boundary. Each sprint unlocks one new capability (an "epic") for your crew design — you don't redesign from scratch each time, you extend what you already have.

| Exercise(s) | Unlocks | Milestone |
| --- | --- | --- |
| [01](01-agentic-frameworks.md) | Agents, tasks, sequential process | **M0: Baseline** |
| [02](02-tool-use.md) | Tool use | **M1: Tools** |
| [03](03-agentic-rag.md) | Knowledge sources / RAG | **M2: RAG** *(interim submission due here)* |
| [04](04-multi-agent-pattern.md) | Multi-agent/hierarchical process | **M3: Multi-agent** |
| [05](05-production.md) + [06](06-securing-agents.md) | Production concerns, security threat modeling | **Final: Production and security** |

Two submissions: an **interim submission** at M2 (formative, lighter weight — catches weak foundations early) and a **final submission** after the last exercise (the full design plus a retrospective on how your thinking changed).

## Team setup: repos and accounts

This course runs in a GitHub Organization, with **one private repository per team — not one per student.** You don't create this repo yourself; your instructor already generated it from the course template, one per team, and grants your team access to it once you're enrolled. See the main [README's "Getting access" section](../../README.md#getting-access-students) for the enrollment steps (GitHub account → team sign-up issue → accept invite).

**Every team member still needs their own GitHub account**, added to the team in the organization (not just to a repo directly). Two reasons: your individual commits are how contribution within the team gets assessed, and a real commit history under your own account is worth having beyond this course.

### Collaborating without git experience

You don't need branches or pull requests for day-to-day team work — one simple loop is enough:

1. Edit a file normally (in your Codespace).
2. Open the **Source Control** panel (the branching-lines icon in the sidebar).
3. Type a one-line commit message, click **✓ Commit**.
4. Click **Sync Changes** — this pulls any teammate's changes and pushes yours, in one step.

No terminal, no `git add`/`commit`/`push` commands. Everyone commits straight to `main`.

To avoid two people editing the same file at once, **divide files between teammates** where you can — e.g. one person owns `agents.yaml`, another `tasks.yaml`. `DESIGN.md` is one shared file everyone contributes to, so for that one specifically: take turns, or commit-and-sync every few minutes rather than both editing it for a long stretch in parallel. If a conflict does happen anyway, VS Code shows a merge view with clickable "Accept Current / Incoming / Both" buttons — ask your instructor for a quick live demo of this once, so it doesn't surprise anyone mid-deadline.

For quick edits (e.g. a `RISK_LOG.md` entry), you can skip Codespaces entirely: open the file on github.com, click the pencil icon, edit in the browser, and click **"Commit changes"** at the bottom.

## Submission package

At each milestone deadline, your submission is the state of your team repo's `main` branch:

| Artifact | Where | What it shows |
| --- | --- | --- |
| Executable crew config | `src/research_crew/config/agents.yaml` + `tasks.yaml` (+ `crew.py` once tools/RAG/process change) | The literal, runnable version of your design |
| Design document | `DESIGN.md` — architecture (agents/tasks/tools/RAG), risks, constraints, security, production considerations, design history | Your full design rationale, critically assessed, in one evolving report |
| Backlog | GitHub Issues (labeled by epic) + a Projects board | Your user stories and progress — lives on GitHub, nothing to export |
| Team notes | `TEAM.md` | Members and who contributed what |
| Optional bonus | a working `crew.py` + a successful `uv run research_crew` | Extra credit only — never required |

Submission is simply **the state of your team repo's `main` branch at the deadline** — there's no pull request to open. Share your repo URL once, at the start; your instructor checks your commit history against each deadline on that same repo (and may tag a specific commit for grading).

## Grading

The design documents (`agents.yaml`/`tasks.yaml` + `DESIGN.md` + backlog) carry the large majority of the grade. Working code is bonus points on top, never a substitute for a thin or missing risk analysis. See [Assignment Milestones](assignment-milestones.md) for the specific risk-analysis prompts graded at each stage.

## Agile practice: backlog and user stories

Run your design process like a real product backlog:
- Each milestone's new capability is an **epic**. Break it into 2–4 **user stories**: *"As a [stakeholder of the crew's output], I want [capability], so that [value]."*
- Write **acceptance criteria** for each story as testable conditions — these double as a draft of the task's `expected_output` field once you get to the YAML, which is a useful thing to notice in itself.
- Add "risks identified and mitigation documented" to every epic's definition of done, so risk analysis is a habit, not a one-off essay.
- If your team is larger than two, rotate a facilitator role each sprint.

Templates for all of this are in [Assignment Templates](assignment-templates.md); a full sprint-by-sprint breakdown (planning checklist, Definition of Done, review, retrospective) is in the [Sprint Plan](assignment-sprint-plan.md).

## For instructors

This is the one-time setup behind everything above. GitHub Classroom stopped taking new sign-ups in May 2026, so this replaces it with plain GitHub Organization features — Free plan covers all of it (unlimited members, unlimited private repos).

### 1. Create the organization and teams

Create a Free organization, then **Settings → Teams → New team** once per project group (e.g. `team-a`, `team-b`, ...). Optionally nest them all under one parent team (e.g. `students`) if you want a shared resources repo visible to everyone automatically — child teams inherit whatever the parent can see.

### 2. Mark this repo as a template, then generate one repo per team

This repo's **Settings → check "Template repository"**. Then per team:
```bash
gh repo create <org>/<team-slug>-crew --template <org>/<this-repo> --private
gh api repos/<org>/<team-slug>-crew/teams/<team-slug> -X PUT -f permission=admin
```
**Admin** (not just Write) matters here — managing a repo's secrets requires Admin, and you want each team able to set up their own API keys without you in the loop.

### 3. Enable Codespaces for the organization

**Org Settings → Codespaces → General** → enable for all repositories (or select the team repos specifically). On the Free plan, Codespaces usage bills to each student's own personal free quota, not the organization — no spending limit to configure.

### 4. Maintain the roster, then set up automatic team enrollment

Students submit only their **GitHub username** via a [team sign-up issue](../../.github/ISSUE_TEMPLATE/team-signup.yml) on this repo — they never choose their own team, on purpose. A [workflow](../../.github/workflows/add-to-team.yml) looks up which team they belong to from [.github/team-roster.csv](../../.github/team-roster.csv) and adds them automatically, so a student can't accidentally (or deliberately) join a team they weren't assigned to.

1. **Fill in the roster before opening sign-ups**: edit `.github/team-roster.csv`, one `github_username,team` row per student, once teams are finalized. Commit it directly — it's not secret, just a class list.
2. **Create the automation's token**: a personal access token with **organization → Members: Read and write** and **repository → Issues: Read and write** scopes (fine-grained), or `admin:org` + `repo` (classic) — needed because team membership is an organization-level permission the default `GITHUB_TOKEN` can't grant.
3. Add it as a secret named `ORG_ADMIN_TOKEN` — either on this repo specifically (**Settings → Secrets and variables → Actions**) or at the org level scoped to this repo (**Org Settings → Secrets and variables → Actions**).
4. That's it — the workflow handles roster lookup, adding, replying, and closing the issue automatically. A username not yet in the roster gets a clear comment telling them to contact you, rather than being added to whatever team they might have guessed.

### 5. Ongoing: review submissions

Check each team's commit history on `main` at each deadline — tag a specific commit yourself (Releases → "Create a new release") if you want an immutable snapshot for grading. Solutions aren't included on purpose, the same as the rest of this series.
