---
name: explain-paper
description: Explain any of the 30 Sutskever reading list papers in a structured 5-part format
license: educational
allowed-tools: arxiv_fetcher github_reader
metadata:
  author: pageman
  version: "0.1.0"
  category: education
---

# Skill: explain_paper

## Purpose
Explain a paper from the Sutskever reading list using a structured 5-part format:
Problem → Key Insight → Math → NumPy Implementation → Historical Context.

## Input
- A paper number (1–30), title, nickname, or arXiv ID

## Steps

1. **Locate in paper_index.yaml**
   Look up the paper in `knowledge/paper_index.yaml` (already in context after on_start hook).
   Extract: canonical title, authors, year, arxiv_id, notebook filename, key_concepts,
   prerequisites, related papers, cluster.

2. **Fetch abstract via arxiv_fetcher**
   Call arxiv_fetcher with the arxiv_id from step 1.
   Use the returned abstract, author list, and publication date to anchor the explanation
   in the paper's own language. Never paraphrase the abstract without quoting it.

3. **Check no_spoilers rule**
   Before revealing the Key Insight, ask the learner one question about the motivating
   problem. Only reveal the insight after they have engaged with the problem.

4. **Structure the explanation in 5 sections**

   ### Problem
   What was broken or missing before this paper? What task could not be solved well?
   Describe the failure mode concretely (e.g., vanishing gradients, fixed-size context vector).

   ### Key Insight
   The single core idea the paper introduces. One sentence. Then unpack it.
   Cite the specific section of the paper: [Paper N: Title, §X.X]

   ### Math
   The central equation(s). Define every variable before using it.
   Use notation from knowledge/notation_guide.md.
   Delegate to math_explainer sub-agent if derivation involves non-standard operators
   or multi-step Jacobian computations.

   ### NumPy Implementation
   How the math maps to the notebook. Reference the notebook filename and key cell indices.
   Highlight the central NumPy operation (e.g., "scaled dot-product via np.matmul").
   Use shape annotations in the format `# (batch, seq_len, d_model)`.

   ### Historical Context
   What came before this paper (prerequisites[] from paper_index.yaml).
   What came after (related[] from paper_index.yaml).
   One sentence on how this paper changed the field.

5. **Cross-link to related papers**
   After the 5 sections, list the related papers from paper_index.yaml with one-line descriptions
   of the connection. Help the learner see where this paper fits in the 30-paper arc.

## Output Format

Use headers: `## Problem`, `## Key Insight`, `## Math`, `## NumPy Implementation`, `## Historical Context`

Every factual claim cites its source per rules/cite_sources.md.
All code examples are NumPy only per rules/numpy_only.md.
