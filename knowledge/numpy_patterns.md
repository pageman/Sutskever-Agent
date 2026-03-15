# NumPy Patterns Reference

Recurring NumPy idioms used across the 30 notebooks.
Each pattern includes: canonical implementation, shape annotations, common mistakes, paper references.

---

## 1. Numerically Stable Softmax

**Papers:** 13, 14, 16, 28, 30 and any paper with attention

```python
def softmax(x):
    # x shape: (..., vocab_size) or (..., seq_len)
    x_shifted = x - x.max(axis=-1, keepdims=True)  # subtract max for stability
    exp_x = np.exp(x_shifted)
    return exp_x / exp_x.sum(axis=-1, keepdims=True)
```

Common mistake: `np.exp(x) / np.exp(x).sum()` — explodes for large x values.
Why stable: subtracting max does not change the output (cancels in numerator and denominator)
but prevents overflow in np.exp().

---

## 2. Batched Matrix Multiplication

**Papers:** 13, 14, 16, 18, 28

Three equivalent approaches:

```python
# Option 1: @ operator (recommended for 2D/3D)
output = Q @ K.T          # (batch, seq, d_k) @ (batch, d_k, seq) → (batch, seq, seq)

# Option 2: np.matmul
output = np.matmul(Q, K.transpose(0, 2, 1))

# Option 3: np.einsum (most explicit, best for complex contractions)
output = np.einsum('bqd,bkd->bqk', Q, K)  # batch query-key attention scores
```

Shape annotation required: always comment the contraction dimensions.

---

## 3. Gradient Accumulation (Manual Backprop)

**Papers:** 2, 3, 4, 13, 14, 18

```python
# Initialize gradients to zero
dW = np.zeros_like(W)
db = np.zeros_like(b)

# Accumulate over sequence steps (BPTT)
for t in reversed(range(T)):
    dW += np.outer(delta[t], x[t])   # outer product accumulation
    db += delta[t]
    dx[t] = W.T @ delta[t]           # propagate to previous layer
```

Common mistake: forgetting to zero gradients before accumulation.
Paper 18 has ~1100 lines of this pattern across multiple attention heads.

---

## 4. Xavier / He Initialization

**Papers:** 7, 10, 11, 13, 15, 26

```python
# Xavier (Glorot) — for tanh/sigmoid activations
W = np.random.randn(fan_in, fan_out) * np.sqrt(2.0 / (fan_in + fan_out))

# He — for ReLU activations
W = np.random.randn(fan_in, fan_out) * np.sqrt(2.0 / fan_in)
```

---

## 5. Convolution via stride_tricks

**Papers:** 7, 10, 11, 15, 26

```python
from numpy.lib.stride_tricks import as_strided

def im2col(x, filter_h, filter_w, stride=1):
    # x shape: (batch, channels, height, width)
    batch, C, H, W = x.shape
    out_h = (H - filter_h) // stride + 1
    out_w = (W - filter_w) // stride + 1

    shape = (batch, C, out_h, out_w, filter_h, filter_w)
    strides = (x.strides[0], x.strides[1],
               stride * x.strides[2], stride * x.strides[3],
               x.strides[2], x.strides[3])

    patches = as_strided(x, shape=shape, strides=strides)
    return patches.reshape(batch, C * filter_h * filter_w, out_h * out_w)
```

This is the key performance trick: converts convolution to matmul.

---

## 6. Gradient Clipping

**Papers:** 2, 3, 4, 18 (any paper with RNN backprop through time)

```python
# Clip all parameter gradients to prevent explosion
clip_value = 5.0
for param_name in gradients:
    gradients[param_name] = np.clip(gradients[param_name], -clip_value, clip_value)
```

When to use: any manual backprop through time (BPTT) that does not use LSTMs.
Even LSTM papers clip as a safety measure (Paper 2 clips at ±5).

---

## 7. Broadcasting for Attention Score Computation

**Papers:** 13, 14, 16, 28, 30

```python
# Scaled dot-product attention
# Q: (batch, heads, seq_q, d_k)
# K: (batch, heads, seq_k, d_k)
scores = np.matmul(Q, K.transpose(0, 1, 3, 2))  # (batch, heads, seq_q, seq_k)
scores = scores / np.sqrt(d_k)                    # scale

# Optional: apply causal mask (for GPT-style models)
mask = np.triu(np.ones((seq_q, seq_q)), k=1).astype(bool)
scores = np.where(mask, -1e9, scores)             # -inf before softmax

attn_weights = softmax(scores)                    # (batch, heads, seq_q, seq_k)
output = np.matmul(attn_weights, V)               # (batch, heads, seq_q, d_v)
```

---

## 8. Sequence Padding and Masking

**Papers:** 3, 13, 14, 21

```python
# Create padding mask: 1 where token is real, 0 where padded
padding_mask = (input_ids != pad_token_id).astype(float)  # (batch, seq_len)

# Expand for broadcasting with attention scores
padding_mask = padding_mask[:, np.newaxis, np.newaxis, :]  # (batch, 1, 1, seq_len)

# Apply: set padded positions to -inf before softmax
scores = scores + (1 - padding_mask) * (-1e9)
```

---

## 9. LSTM Gate Computation (Vectorized)

**Papers:** 2, 3, 4, 18, 20

```python
def lstm_step(x_t, h_prev, c_prev, W, b):
    # x_t:   (batch, input_dim)
    # h_prev: (batch, H)
    # W:      (input_dim + H, 4 * H)  — all four gates fused
    # b:      (4 * H,)

    z = np.concatenate([x_t, h_prev], axis=1)    # (batch, input_dim + H)
    gates = z @ W + b                             # (batch, 4 * H)

    # Split into four gates
    f, i, g, o = np.split(gates, 4, axis=1)      # each: (batch, H)

    f = sigmoid(f)    # forget gate
    i = sigmoid(i)    # input gate
    g = np.tanh(g)    # candidate
    o = sigmoid(o)    # output gate

    c = f * c_prev + i * g    # (batch, H)
    h = o * np.tanh(c)        # (batch, H)

    return h, c
```

The fused W matrix (pedagogical notebooks often use separate matrices for clarity).

---

## 10. Numerical Gradient Checking

**Papers:** 18 (used to verify the 1100-line backward pass)

```python
def numerical_gradient(loss_fn, param, epsilon=1e-5):
    grad = np.zeros_like(param)
    it = np.nditer(param, flags=['multi_index'])
    while not it.finished:
        idx = it.multi_index
        original = param[idx]

        param[idx] = original + epsilon
        loss_plus = loss_fn()

        param[idx] = original - epsilon
        loss_minus = loss_fn()

        grad[idx] = (loss_plus - loss_minus) / (2 * epsilon)
        param[idx] = original
        it.iternext()

    return grad

# Compare analytical vs numerical gradient
diff = np.max(np.abs(analytical_grad - numerical_grad)) / \
       (np.max(np.abs(analytical_grad)) + np.max(np.abs(numerical_grad)) + 1e-8)
assert diff < 1e-5, f"Gradient check failed: relative diff = {diff}"
```
