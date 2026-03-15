---
name: compare-papers
description: Compare two or more papers side-by-side with a table and prose synthesis
license: MIT
allowed-tools: arxiv_fetcher github_reader
metadata:
  author: pageman
  version: "0.1.0"
  category: education
---

# Skill: compare_papers

## Purpose
Compare two or more papers from the Sutskever reading list: build a comparison table,
write a prose synthesis of their conceptual relationship, and identify shared NumPy idioms.

## Input
- Two or more paper numbers, titles, or nicknames

## Steps

1. **Look up each paper in paper_index.yaml**
   For each paper: extract title, year, key_concepts, numpy_highlight, cluster, prerequisites, related.

2. **Fetch abstracts via arxiv_fetcher**
   Call arxiv_fetcher for each paper. Use the abstracts to anchor comparisons in the papers'
   own language. Note what problem each paper states it solves.

3. **Extract comparison dimensions**
   For each paper, determine:
   - The problem it solves
   - Its core mechanism (the key architectural or algorithmic idea)
   - Its central equation (reference notation_guide.md for consistency)
   - The NumPy complexity (simple matmul vs. complex stride_tricks vs. manual backprop)
   - Its primary limitation (what the next paper in the lineage fixes)

4. **Build comparison table**
   Format:
   | Dimension | Paper A | Paper B | ... |
   |-----------|---------|---------|-----|
   | Problem   |         |         |     |
   | Mechanism |         |         |     |
   | Key Equation |      |         |     |
   | NumPy Complexity |  |         |     |
   | Limitation |        |         |     |

5. **Write prose synthesis**
   3–5 sentences answering:
   - What conceptual thread connects these papers?
   - What does each one add to the lineage?
   - If the papers are in the same cluster (from sutskever_reading_list.md), explain
     the cluster's unifying theme.

6. **Identify shared NumPy idioms**
   Check knowledge/numpy_patterns.md. Which patterns appear in both notebooks?
   (e.g., "Both papers use softmax attention via the log-sum-exp stable pattern.")

7. **Recommend reading order**
   Based on prerequisites[] and related[] from paper_index.yaml, suggest which paper
   to read first and why.

## Output Format
Comparison table, then prose synthesis, then shared idioms section, then reading order recommendation.
Every paper reference uses `[Paper N: Title (Year)]`.
