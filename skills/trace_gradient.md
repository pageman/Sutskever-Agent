---
name: trace_gradient
description: Walk the chain rule backwards from loss to input for any notebook's backprop cells
license: MIT
allowed-tools: notebook_parser github_reader
metadata:
  author: pageman
  version: "0.1.0"
  category: education
---

# Skill: trace_gradient

## Purpose
Trace the backpropagation chain rule from the loss function through all layers to the inputs.
Provide both the mathematical derivation and annotated NumPy code for each gradient step.

## Input
- A paper/notebook number, optionally a specific layer or operation to focus on

## Steps

1. **Fetch and parse notebook**
   Use github_reader to fetch the notebook, notebook_parser to extract all cells.
   If the notebook is already in context from explain_notebook, skip the fetch.

2. **Locate gradient computation cells**
   Scan all code cells for patterns: `grad`, `dW`, `d_`, `delta`, `backward`,
   explicit loss derivative computations, `np.clip` with gradient clipping values.
   List all matching cell indices.

3. **Express each gradient in mathematical notation**
   For each gradient cell, write the computation in:
   (a) Mathematical notation — matching knowledge/notation_guide.md conventions
   (b) Pseudocode — one line per operation, with shape annotations
   (c) The actual NumPy code from the cell

4. **Walk the chain rule backwards**
   Starting from the loss, trace:
   loss → output layer gradients → hidden layer gradients → input gradients
   At each step: state the chain rule application explicitly.
   Format: `∂L/∂W = ∂L/∂output · ∂output/∂W`

5. **Delegate non-standard operators to math_explainer**
   If the gradient involves:
   - LSTM gate Jacobians (diag(f_t) terms)
   - Attention softmax gradient (∂w_i/∂z_i = w_i(1 - w_i))
   - Variational ELBO gradient (reparameterization trick)
   - CTC forward-backward algorithm
   → Delegate to math_explainer sub-agent for that sub-derivation.

6. **Special handling: Paper 18 (Relational RNN, ~1100 lines of manual backprop)**
   For Paper 18 only: first explain the macro structure (which gradient flows where),
   then offer to drill into any specific sub-component. Do not attempt to walk all
   1100 lines in a single response.

7. **Highlight numerical stability tricks**
   For every gradient cell, check:
   - Is log-sum-exp used for numerically stable softmax?
   - Is gradient clipping present? What threshold?
   - Is layer normalization applied before or after the gradient step?
   - Any finite-difference gradient checking cells?
   Note each trick and explain why it is necessary.

## Output Format
An annotated equation chain (math notation → pseudocode → NumPy), then a prose summary
of the full gradient flow. Delegate sub-derivations to math_explainer where applicable.
Reference knowledge/numpy_patterns.md §Gradient Clipping and §Gradient Accumulation.
