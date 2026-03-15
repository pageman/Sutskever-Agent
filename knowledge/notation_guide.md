# Notation Guide

Canonical mathematical notation used across all 30 notebooks and this agent's explanations.
All explanations must use these conventions to ensure consistency.

---

## Linear Algebra

| Symbol | Meaning | NumPy |
|--------|---------|-------|
| **W** | Weight matrix (bold uppercase) | `W` |
| **b** | Bias vector (bold lowercase) | `b` |
| **x** | Input vector | `x` |
| **h** | Hidden state vector | `h` |
| ⊙ | Elementwise (Hadamard) product | `*` or `np.multiply` |
| · | Matrix multiplication | `@` or `np.matmul` |
| ᵀ | Transpose | `.T` |

## Shape Annotation Convention

Always annotate shapes in comments:
```python
x = np.random.randn(batch, seq_len, d_model)  # (batch, seq_len, d_model)
```

Use named dimensions, not numbers, wherever possible.

---

## Activation Functions

| Symbol | Name | NumPy |
|--------|------|-------|
| σ(x) | Sigmoid | `1 / (1 + np.exp(-x))` |
| tanh(x) | Hyperbolic tangent | `np.tanh(x)` |
| ReLU(x) | Rectified Linear | `np.maximum(0, x)` |
| softmax(x) | Softmax (stable) | `np.exp(x - x.max()) / np.exp(x - x.max()).sum()` |

---

## Gradient Notation

| Math | Code | Meaning |
|------|------|---------|
| ∂L/∂W | `dL_dW` or `dW` | Gradient of loss w.r.t. W |
| ∂L/∂x | `dL_dx` or `dx` | Gradient of loss w.r.t. x |
| δ | `delta` | Error signal (pre-activation gradient) |

---

## RNN / LSTM Notation

| Symbol | Meaning |
|--------|---------|
| h_t | Hidden state at time t — shape: (batch, H) |
| c_t | Cell state at time t — shape: (batch, H) |
| x_t | Input at time t — shape: (batch, input_dim) |
| f_t | Forget gate output — shape: (batch, H) |
| i_t | Input gate output — shape: (batch, H) |
| g_t | Candidate cell values — shape: (batch, H) |
| o_t | Output gate output — shape: (batch, H) |
| W_h | Recurrent weight matrix — shape: (H, H) |
| W_x | Input weight matrix — shape: (input_dim, H) |

---

## Attention Notation (Papers 6, 13, 14, 16, 28, 30)

| Symbol | Meaning | Shape |
|--------|---------|-------|
| Q | Query matrix | (batch, seq_q, d_k) |
| K | Key matrix | (batch, seq_k, d_k) |
| V | Value matrix | (batch, seq_v, d_v) |
| d_k | Key/query dimension | scalar |
| A | Attention weights | (batch, seq_q, seq_k) |

Central equation:
```
A = softmax(Q @ K.T / sqrt(d_k))
output = A @ V
```

---

## VAE Notation (Paper 17)

| Symbol | Meaning |
|--------|---------|
| μ | Encoder mean output |
| σ | Encoder std output (log σ² in practice) |
| z | Latent sample: z = μ + σ ⊙ ε, ε ~ N(0,I) |
| ELBO | Evidence Lower BOund: E[log p(x|z)] - KL(q(z|x) ‖ p(z)) |

Note: Paper 17 uses μ/σ for encoder outputs. This notation does NOT conflict with
the σ() sigmoid activation — context disambiguates.

---

## Disambiguation: Notation Conflicts Across Papers

| Symbol | In Paper(s) | Meaning |
|--------|-------------|---------|
| σ | Most papers | Sigmoid activation function |
| σ | Paper 17 (VAE) | Encoder standard deviation output |
| h | RNN papers (2,3,4,18,20) | Hidden state |
| h | Vision papers (7,10,11,15,26) | Feature map height dimension |
| d | Attention papers (13,14,16) | Model dimension |
| d | Information theory papers (5,8,23) | Kolmogorov complexity or description length |

When the context is ambiguous, this agent will always clarify which meaning is in use.
