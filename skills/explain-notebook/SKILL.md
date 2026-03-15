---
name: explain-notebook
description: Walk through a notebook cell-by-cell with shape annotations and gradient moment identification
license: educational
allowed-tools: github_reader notebook_parser
metadata:
  author: pageman
  version: "0.1.0"
  category: education
---

# Skill: explain_notebook

## Purpose
Provide a cell-by-cell walkthrough of a notebook from pageman/sutskever-30-implementations,
annotating each code cell with: the central NumPy operation, why it was chosen, and shape
annotations at each step.

## Input
- A notebook number (1–30) or filename

## Steps

1. **Resolve notebook filename**
   Look up the notebook filename in `knowledge/paper_index.yaml` using the provided number.

2. **Fetch notebook via github_reader**
   ```
   tool: github_reader
   input:
     repo: pageman/sutskever-30-implementations
     path: <notebook_filename>
     ref: main
     operation: read_file
   ```

3. **Parse notebook via notebook_parser**
   ```
   tool: notebook_parser
   input:
     content: <raw ipynb JSON from step 2>
     filter_cell_type: all
     include_outputs: true
   ```

4. **Identify the gradient moment**
   Scan parsed cells for patterns: `grad`, `dW`, `delta`, `backward`, loss derivative patterns.
   Flag the first cell where backpropagation begins. Note the cell index for trace_gradient skill.

5. **Walk through cells in order**
   For each code cell:
   - State what the cell accomplishes in one sentence
   - Identify the central NumPy operation (matmul, einsum, stride_tricks, etc.)
   - Explain *why* that operation was chosen (not just what it does)
   - Add shape annotations for every array: `# (batch, seq_len, d_model)`
   - Note any numerical stability patterns (log-sum-exp, clipping, normalization)
   - Reference knowledge/numpy_patterns.md for recurring idioms

   For each markdown cell:
   - Summarize what concept the cell introduces
   - Flag if the cell references a specific equation from the paper

6. **Identify the pedagogical arc**
   After the cell walkthrough, write a prose summary (3–5 sentences):
   What concept is the notebook building toward? How does each section advance it?
   What is the "aha moment" cell where the full algorithm comes together?

7. **Flag gradient moment for follow-up**
   Inform the learner: "Cell N contains the backward pass — use /trace_gradient
   to walk through the chain rule in detail."

## Output Format
Numbered cell annotations (Cell 0, Cell 1, ...), then a prose summary section.
Cite cells as `[nb:N cell:M]`.
All code in annotations is NumPy only.
