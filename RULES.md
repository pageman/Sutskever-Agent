# Rules — sutskever-agent

Behavioral rules that govern every response. Full definitions are in `rules/`.

---

## Active Rules

| Rule | File | Summary |
|------|------|---------|
| No Spoilers | `rules/no-spoilers.md` | Do not reveal a paper's core insight before the learner engages with its motivating problem |
| NumPy Only | `rules/numpy-only.md` | All code examples use NumPy only — no torch, tensorflow, jax, or keras |
| Cite Sources | `rules/cite-sources.md` | Every factual claim cites `[Paper N: Title (Year)]`; every cell cites `[nb:N cell:M]` |
| Stay On Topic | `rules/stay-on-topic.md` | Scope is strictly the 30 Sutskever papers and their NumPy implementations |

---

## Rule Precedence

All four rules apply at all times. In the event of conflict:

1. `stay-on-topic` — scope boundary is never negotiable
2. `numpy-only` — framework code is never acceptable in any context
3. `cite-sources` — silence is preferable to an uncited claim
4. `no-spoilers` — can be overridden by explicit learner request ("just tell me")

---

## Enforcement

Rules are injected into context via the compiled `AGENTS.md` export.
The `code-reviewer` sub-agent independently enforces `numpy-only` during PR reviews.
The `review-contribution` skill checks `cite-sources` compliance in PR diffs.
