---
name: generate-exercises
description: Generate 3-tier exercises (Comprehension, Extension, Research) for any paper/notebook
license: MIT
allowed-tools: github_reader notebook_parser
metadata:
  author: pageman
  version: "0.1.0"
  category: education
---

# Skill: generate_exercises

## Purpose
Generate exercises at three difficulty tiers for any paper or notebook.
Exercises must be solvable using only NumPy — no framework imports.

## Input
- A paper number, title, or notebook number

## Steps

1. **Fetch and parse the notebook**
   Use github_reader to fetch the notebook, then notebook_parser to extract the cell structure.
   Read through all cells to understand: what concepts are implemented, what is left as-is
   from the paper (not modified), what edge cases exist.

2. **Check prerequisites**
   Look up the paper in paper_index.yaml. Read prerequisites[] to understand what background
   the learner is assumed to have. Exercises should not assume knowledge beyond prerequisites.

3. **Generate Tier 1: Comprehension exercises**
   Goal: verify the learner can read and understand the existing implementation.
   Format: "What does [specific line/cell] compute? Verify by [small modification]."
   - Each exercise references a specific cell: `[nb:N cell:M]`
   - Each exercise has a one-sentence expected output/behavior
   - Each exercise has a hidden hint in a markdown details block

4. **Generate Tier 2: Extension exercises**
   Goal: the learner modifies or extends the existing implementation.
   Format: "Modify the implementation to support Y. You will need to: [step list]."
   - Extensions must stay within the paper's architectural assumptions
   - All code must remain NumPy only
   - Each extension includes: what to change, what to verify, expected impact on loss/performance

5. **Generate Tier 3: Research exercises**
   Goal: the learner tests a hypothesis from the paper or a natural extension of it.
   Format: "The paper claims/assumes X. Test this hypothesis: [specific measurable experiment]."
   - Reference specific claims from the paper using [Paper N: §X.X]
   - Include: hypothesis, experiment design, what result would confirm/refute, NumPy implementation sketch

6. **Validate NumPy constraint**
   Review all generated exercises. Confirm no exercise requires torch, tensorflow, jax, or keras.
   If an exercise would be much easier with a framework, add a note: "This is intentionally
   harder in NumPy — that difficulty is the point."

## Output Format
Three clearly labeled sections: `### Tier 1: Comprehension`, `### Tier 2: Extension`, `### Tier 3: Research`.
Present Tier 1 first. Offer Tiers 2 and 3 only after the learner completes Tier 1.
All hints in `<details>` blocks. All cell references use `[nb:N cell:M]` format.
