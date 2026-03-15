---
name: summarize-repo
description: Generate a navigable overview of all 30 papers organized by learning track
license: educational
allowed-tools: github_reader
metadata:
  author: pageman
  version: "0.1.0"
  category: education
---

# Skill: summarize_repo

## Purpose
Generate a navigable summary of pageman/sutskever-30-implementations organized by
learning track, with optional filtering by topic cluster or difficulty.

## Input
- Optional filter: track name (Beginner/Intermediate/Advanced/Theory), cluster name, or difficulty label

## Steps

1. **Load sutskever_reading_list.md**
   This file is in knowledge/ and loaded in context. Extract:
   - All 30 papers with their track assignments
   - The four thematic clusters
   - Suggested reading order per track

2. **Load paper_index.yaml**
   Already in context (loaded by on_start hook). Use for:
   - difficulty labels per paper
   - estimated_hours per paper
   - key_concepts per paper
   - numpy_highlight per paper

3. **Fetch source repo README for updates**
   ```
   tool: github_reader
   input:
     repo: pageman/sutskever-30-implementations
     path: README.md
     ref: main
     operation: read_file
   ```
   Check if the source repo README lists any updates, new notebooks, or errata.
   If the README has additional track guidance, incorporate it.

4. **Apply filter if provided**
   If the user requests a specific track: include only papers in that track.
   If the user requests a cluster: include only papers in that cluster.
   If no filter: include all 30 papers, organized by track.

5. **Generate summary**
   For each track section:
   - Track name and estimated total hours
   - Papers in suggested reading order
   - Per paper: number, title, one-sentence description, key NumPy concept, difficulty, estimated hours

6. **Include "start here" recommendation**
   If the user provided background information: recommend the specific entry point.
   If no background provided: default recommendation is Paper 2 (Char-RNN) for Intermediate,
   Paper 7 (LeNet/AlexNet) for Beginner visual learners.

7. **Include thematic cluster map**
   After the per-track breakdown, show the four clusters as a mini-map so the learner
   can see cross-track connections.

## Output Format
A markdown table of contents, then per-track sections with paper tables.
End with the cluster map and a "start here" recommendation.
