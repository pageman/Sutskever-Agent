---
name: review-contribution
description: Review a PR or diff to sutskever-30-implementations for correctness and pedagogical structure
license: educational
allowed-tools: github_reader notebook_parser
metadata:
  author: pageman
  version: "0.1.0"
  category: review
---

# Skill: review_contribution

## Purpose
Review a contribution (PR diff or branch) to pageman/sutskever-30-implementations
for: algorithmic correctness, NumPy compliance, pedagogical structure, and gradient integrity.

## Input
- A PR number, branch name, or diff content

## Steps

1. **Fetch the diff via github_reader**
   ```
   tool: github_reader
   input:
     repo: pageman/sutskever-30-implementations
     operation: read_pr
     pr_number: <number>
   ```

2. **Identify which notebook is modified**
   Parse the diff file list. Map to paper_index.yaml to get the paper context.

3. **Delegate to code_reviewer sub-agent**
   Hand off: the diff, the notebook context (paper title, key_concepts, numpy_highlight),
   and the relevant entries from knowledge/numpy_patterns.md.
   The code_reviewer sub-agent returns CRITICAL / WARNING / SUGGESTION findings.

4. **Check NumPy compliance (rules/numpy_only.md)**
   Scan the diff for disallowed imports: torch, tensorflow, tf, jax, keras.
   Any match is an immediate CRITICAL finding. sklearn is permitted only for data utilities.

5. **Check pedagogical structure**
   The expected notebook structure is: motivation cell → math cell → implementation cells → test cell → visualization cell.
   Verify the contribution maintains or extends this structure.
   Flag if visualization cells are inserted before test cells (incorrect order).
   Flag if new markdown cells lack paper citations per rules/cite_sources.md.

6. **Gradient audit**
   If the diff touches any cell containing backpropagation (grad, dW, delta patterns):
   invoke trace_gradient skill on the modified cells.
   Verify: scaling factors present (√d_k for attention), gradient clipping present where needed,
   no numerically unstable operations (unclipped softmax on large logits).

7. **Compile findings**
   Aggregate all findings from steps 3–6 into a single structured review using this format:

   ```
   ## Correctness
   [CRITICAL/WARNING/SUGGESTION] finding — explanation — fix — paper citation

   ## NumPy Compliance
   [findings]

   ## Pedagogical Structure
   [findings]

   ## Gradient Check
   [findings]

   ## Summary
   N CRITICAL, N WARNING, N SUGGESTION
   ```

8. **Human gate**
   If any CRITICAL findings exist, do not post the review automatically.
   Present the compiled review to the user and request explicit approval before posting.

## Output Format
Structured review with severity labels. Every finding cites the relevant rule file or paper.
CRITICAL findings must include a specific fix, not just identification of the problem.
