# Risk Assessment — sutskever-agent v0.1.0

## Classification

**Risk Tier: LOW**

This agent is an educational tool. It does not operate in any regulated domain.

---

## Risk Factors Evaluated

| Factor | Present | Notes |
|--------|---------|-------|
| Financial decisions or recommendations | No | Out of scope per `rules/stay-on-topic.md` |
| Medical or safety-critical outputs | No | Out of scope |
| Legal advice | No | Out of scope |
| PII processing or storage | No | No user data collected beyond local session notes |
| Autonomous write operations | Conditional | PR comments require explicit human approval |
| External API calls | Yes (low risk) | arXiv (read-only, public) and GitHub (read + gated write) |
| Model hallucination risk | Low-medium | Mitigated by `rules/cite-sources.md` and paper_index.yaml grounding |
| Scope creep risk | Low | Mitigated by `rules/stay-on-topic.md` |

---

## Residual Risks

1. **Citation hallucination** — Agent may misattribute a claim to the wrong paper section.
   Mitigation: `arxiv-fetcher` tool grounds abstracts in primary sources.

2. **Incorrect gradient derivation** — Mathematical steps may contain errors.
   Mitigation: `math-explainer` sub-agent (temp: 0.2) is used for all non-trivial derivations.
   Users should verify against original papers for any production use.

3. **GitHub token exposure** — The `github-reader` tool requires a token with repo scope.
   Mitigation: token is read from environment variable `GITHUB_TOKEN`, never hardcoded.

---

## Review Schedule

Re-assess if:
- Agent scope is expanded beyond educational use
- Agent gains autonomous write access beyond PR comments
- A new risk tier is introduced in the gitagent spec
