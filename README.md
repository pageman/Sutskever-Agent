# sutskever-agent

**A [GitAgent](https://www.gitagent.sh/) definition providing an AI pedagogue layered on [pageman/sutskever-30-implementations](https://github.com/pageman/sutskever-30-implementations)**

![Skills](https://img.shields.io/badge/skills-7-blue) ![Spec](https://img.shields.io/badge/gitagent-v0.1.0-green) ![Validation](https://img.shields.io/badge/validation-passing-brightgreen) ![Model](https://img.shields.io/badge/model-claude--sonnet--4--6-blueviolet)

This repo **does not contain notebooks**. It defines an AI agent that reads, explains, traces, and reviews the 30 pure-NumPy deep learning implementations in the companion repository. Each skill is:

- Grounded in the original paper via arXiv fetching — no hallucinated citations
- Anchored to the actual notebook cells via GitHub API reads
- Structured with a consistent 5-part explanation format
- Governed by explicit rules (no spoilers, NumPy-only, cite sources)
- Delegatable to specialist sub-agents (math derivations, code review)

---

## Quick Start

```bash
# Prerequisites: Node.js >= 18, a GitHub token
npm install -g @shreyaskapale/gitagent

git clone https://github.com/pageman/sutskever-agent
cd sutskever-agent
gitagent validate

# Export and run with Claude Code
gitagent export --format claude-code --output exports/claude-code
claude --system-prompt exports/claude-code
```

---

## Skills

| # | Skill | Description | Tools |
|---|-------|-------------|-------|
| 1 | `explain-paper` | 5-part explanation: Problem → Key Insight → Math → NumPy → Context | arxiv-fetcher, github-reader |
| 2 | `explain-notebook` | Cell-by-cell walkthrough with shape annotations and gradient moment detection | github-reader, notebook-parser |
| 3 | `compare-papers` | Side-by-side table + prose synthesis of thematic connections | arxiv-fetcher, github-reader |
| 4 | `review-contribution` | PR review: correctness, NumPy compliance, pedagogical structure | github-reader, notebook-parser |
| 5 | `generate-exercises` | 3-tier exercises: Comprehension / Extension / Research | github-reader, notebook-parser |
| 6 | `summarize-repo` | Navigable overview of all 30 papers filtered by track or cluster | github-reader |
| 7 | `trace-gradient` | Chain rule walkthrough from loss to input with stability annotations | notebook-parser, github-reader |

---

## Workflows

| Workflow | Trigger | Description |
|----------|---------|-------------|
| `onboard-new-user` | First session | Assess background, assign learning track, recommend entry point |
| `pr-review-pipeline` | PR opened on source repo | Full technical + pedagogical review with human gate before posting |
| `study-session` | Any session | Guided paper study: explain → walk notebook → trace gradient → exercises → memory |

---

## Sub-Agents

| Agent | Temperature | Role |
|-------|------------|------|
| `math-explainer` | 0.2 | Step-by-step derivations — never skips steps, never hand-waves |
| `code-reviewer` | 0.1 | CRITICAL / WARNING / SUGGESTION findings on NumPy implementations |

---

## Repository Structure

```
sutskever-agent/
├── agent.yaml                  # Root manifest — model, skills, tools, compliance
├── SOUL.md                     # Agent identity, values, communication style
├── skills/                     # 7 skill definitions (explain-paper/, trace-gradient/, ...)
├── tools/                      # 3 tool definitions (github-reader, notebook-parser, arxiv-fetcher)
├── workflows/                  # 3 multi-step workflows
├── knowledge/                  # Static reference: paper index, notation guide, NumPy patterns
├── rules/                      # 4 behavioral guardrails (no-spoilers, numpy-only, ...)
├── hooks/                      # Session lifecycle hooks + shell scripts
├── agents/                     # Sub-agents: math-explainer/, code-reviewer/
├── compliance/                 # Risk assessment, model card
└── .github/workflows/          # CI: gitagent validate on every push
```

---

## Learning Tracks

The agent onboards new users into one of four tracks drawn from the source repo:

**Beginner** — Papers 7 → 10 → 11 → 22 → 26 → 2 → 3 (start: AlexNet, ~21 hours)

**Intermediate** — Papers 2 → 3 → 4 → 6 → 13 → 14 → 16 → 18 → 20 → 22 → 26 → 28 (start: Char-RNN, ~57 hours)

**Advanced** — Papers 5 → 8 → 9 → 12 → 17 → 19 → 21 → 23 → 24 → 25 → 27 → 29 → 30 (start: MDL, ~69 hours)

**Theory** — Papers 5 → 23 → 24 → 25 → 1 → 8 → 19 (start: MDL, ~35 hours)

---

## Key Design Decisions

**Source repo is never modified.** This agent is a pure overlay — it reads `pageman/sutskever-30-implementations` via the GitHub API. No notebooks are changed.

**NumPy-only rule is enforced at every layer.** The `rules/numpy-only.md` rule is applied in skill instructions, exercise generation, and PR reviews. The `code-reviewer` sub-agent flags any `torch`/`jax`/`tensorflow` import as CRITICAL.

**No spoilers by default.** `rules/no-spoilers.md` lists the core "trick" of each paper and prevents the agent from revealing it before the learner has engaged with the motivating problem.

**PR review requires human approval.** The `pr-review-pipeline` workflow includes a human gate: if any CRITICAL finding exists, the compiled review is shown to the user for approval before being posted as a GitHub comment.

**Exports are generated, not committed.** Run `gitagent export --format <fmt> --output exports/<fmt>` to generate adapter-specific versions. Supported: `claude-code`, `openai`, `crewai`, `github`.

---

## Export Targets

```bash
gitagent export --format claude-code  --output exports/claude-code
gitagent export --format openai       --output exports/openai
gitagent export --format crewai       --output exports/crewai
gitagent export --format github       --output exports/github-actions
```

---

## Contributing

This repo follows the [GitAgent v0.1.0 spec](https://www.gitagent.sh/). All PRs run `gitagent validate` via `.github/workflows/validate.yml` — the PR must pass validation before merge.

To add a skill: create `skills/<hyphen-name>/SKILL.md` with the required front-matter, register the name in `agent.yaml` under `skills:`, and run `gitagent validate` locally before opening a PR.

Commit message convention follows the companion repo:
- `feat:` for new skills, tools, or workflows
- `fix:` for corrections
- `docs:` for README and knowledge base updates

---

## Citation

```bibtex
@misc{sutskever-agent-2026,
  author    = {Paul "The Pageman" Pajo, pageman@gmail.com},
  title     = {sutskever-agent: A GitAgent pedagogue for the Sutskever 30-paper reading list},
  year      = {2026},
  url       = {https://github.com/pageman/sutskever-agent},
  note      = {GitAgent v0.1.0 definition layered on pageman/sutskever-30-implementations}
}
```

---

## License

Educational use. See individual papers for original research citations.

---

## Acknowledgments

- [Ilya Sutskever](https://twitter.com/ilyasut) for the original reading list
- [pageman/sutskever-30-implementations](https://github.com/pageman/sutskever-30-implementations) — the companion repository this agent is built on
- [GitAgent](https://www.gitagent.sh/) / [@shreyaskapale](https://github.com/shreyaskapale) for the open agent standard
