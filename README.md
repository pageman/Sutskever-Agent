# sutskever-agent

A [GitAgent](https://www.gitagent.sh/) definition that provides an AI pedagogue
layered on top of [pageman/sutskever-30-implementations](https://github.com/pageman/sutskever-30-implementations).

This repo **does not contain notebooks**. It defines an agent that reads, explains,
and reviews the 30 pure-NumPy notebooks in the source repository.

---

## What This Agent Does

- Explains any of the 30 papers (Problem → Key Insight → Math → NumPy Implementation → Historical Context)
- Walks through notebooks cell-by-cell with shape annotations
- Traces gradient/backprop chains from loss to input
- Generates tiered exercises (Comprehension / Extension / Research)
- Reviews PRs to the source repo for NumPy compliance and pedagogical structure
- Maintains a study session with memory across conversations

---

## Prerequisites

- Node.js >= 18
- `npm install -g gitagent`
- A GitHub token (for reading/reviewing the source repo)

---

## Quickstart

```bash
git clone https://github.com/your-username/sutskever-agent
cd sutskever-agent
gitagent run . --adapter claude-code
```

Or export and use directly with Claude Code:

```bash
gitagent export --format claude-code --output exports/claude-code/
cd exports/claude-code
claude
```

---

## Skills

| Skill | Description |
|-------|-------------|
| `explain_paper` | 5-part paper explanation with arXiv abstract |
| `explain_notebook` | Cell-by-cell walkthrough with shape annotations |
| `compare_papers` | Side-by-side comparison table + synthesis |
| `review_contribution` | PR review: correctness, NumPy compliance, pedagogy |
| `generate_exercises` | 3-tier exercises: Comprehension, Extension, Research |
| `summarize_repo` | Navigable overview filtered by track or topic |
| `trace_gradient` | Chain rule walkthrough from loss to input |

---

## Workflows

| Workflow | Trigger | Description |
|----------|---------|-------------|
| `onboard_new_user` | First session | Assess background, assign track, recommend entry point |
| `pr_review_pipeline` | PR opened on source repo | Full technical + pedagogical review |
| `study_session` | Any session | Guided paper study with exercises and memory |

---

## Sub-Agents

| Agent | Role |
|-------|------|
| `math_explainer` | Derives equations step-by-step; never skips steps |
| `code_reviewer` | Reviews NumPy code for correctness and stability |

---

## Export Targets

```bash
gitagent export --format claude-code      --output exports/claude-code/
gitagent export --format openai           --output exports/openai/
gitagent export --format crewai           --output exports/crewai/
gitagent export --format github-actions   --output exports/github-actions/
```

---

## Contributing

This repo follows the [GitAgent v0.1.0 spec](https://www.gitagent.sh/).
All PRs run `gitagent validate` via `.github/workflows/validate.yml`.

To add a skill: create `skills/<name>.md` with the required front-matter,
then register it in `agent.yaml` under `skills:`.

---

## License

MIT
