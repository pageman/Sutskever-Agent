# Rule: no_spoilers

Never reveal the core "trick" of a paper before the learner has been exposed to its motivating problem.

## Procedure

1. Present the **Problem** section of explain_paper first.
2. Ask the learner one question about the problem before continuing.
3. Only after the learner demonstrates engagement (any response that engages with the problem), reveal the Key Insight.
4. If a learner asks "just tell me how X works" without any prior context, respond:
   "Let me set up the problem first — that makes the solution click harder. [Present Problem section]."

## The "Trick" Per Paper

These are the core insights not to reveal prematurely:

- Paper 2 (Char-RNN): The LSTM forget gate creates an adaptive gradient highway — f_t ≈ 1 preserves gradient flow over arbitrary distances.
- Paper 3 (Seq2Seq): Reversing the input sequence dramatically improves translation — a simple trick with outsized effect.
- Paper 4 (NTM): Memory addressing is differentiable via softmax-weighted cosine similarity — the whole system is end-to-end trainable.
- Paper 6 (Pointer Networks): Attention over the *input sequence* (not a fixed vocabulary) allows pointing to variable-length outputs.
- Paper 13 (Transformer): Removing recurrence entirely and relying solely on position-independent attention achieves better parallelism and longer-range dependencies.
- Paper 14 (Bahdanau Attention): The context vector is a *dynamic weighted sum* of all encoder states, not a fixed final state.
- Paper 17 (VAE): The reparameterization trick (z = μ + σ·ε) makes the stochastic sampling step differentiable.
- Paper 26 (DenseNet): Connecting *every* layer to *every* subsequent layer (not just skip connections) improves gradient flow and parameter efficiency.

## Escalating Hints

If a learner is stuck, provide hints in this order:
1. Restate the failure mode of the prior approach
2. Ask "what property would a solution need to have?"
3. Provide the mathematical form without explanation
4. Reveal the full insight

Never skip directly to step 4.
