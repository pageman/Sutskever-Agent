# Prerequisites

What you need to know before working through the 30 notebooks.

---

## Mathematical Prerequisites

### Essential for all tracks

- **Linear algebra**: matrix multiplication, transpose, dot product, eigenvalues/eigenvectors
- **Calculus**: derivatives, partial derivatives, chain rule
- **Probability**: conditional probability, Bayes' rule, Gaussian distributions

### Required for Intermediate track

- **Backpropagation**: chain rule applied to neural network layers, gradient flow
- **Optimization**: gradient descent, momentum, learning rate schedules

### Required for Advanced track

- **Information theory**: entropy H(X) = -Σ p(x) log p(x), KL divergence, mutual information
- **Probability**: expectation, variance, ELBO, variational inference basics

### Required for Theory track

- **Information theory**: all of the above plus MDL, Kolmogorov complexity
- **Complexity theory**: basic familiarity with Turing machines and computability

---

## NumPy Prerequisites

### Essential

- Array creation: `np.zeros`, `np.ones`, `np.random.randn`
- Indexing and slicing: `x[1:3]`, `x[:, 0]`, `x[..., -1]`
- Basic operations: `+`, `-`, `*`, `/`, `@`, `.T`
- Reduction: `np.sum`, `np.mean`, `np.max` with `axis` parameter

### Important

- **Broadcasting**: how shapes `(3, 1)` and `(1, 4)` combine to `(3, 4)`
- **einsum**: `np.einsum('bij,bjk->bik', A, B)` — explicit contraction notation
- **reshape and transpose**: `x.reshape(batch, -1)`, `x.transpose(0, 2, 1)`

### Advanced (needed for vision papers)

- **stride_tricks**: `np.lib.stride_tricks.as_strided` — used for efficient convolution
- **structured arrays**: occasionally used for complex indexing

---

## Per-Track Prerequisite Map

| Track | Math Needed | NumPy Needed |
|-------|------------|--------------|
| Beginner | Linear algebra, basic calculus | Essential |
| Intermediate | + Backprop, optimization | + Broadcasting, einsum |
| Advanced | + Information theory | + stride_tricks |
| Theory | + Complexity theory, MDL | Standard NumPy sufficient |

---

## Filling Gaps

- **Linear algebra**: Gilbert Strang's MIT OCW lectures (18.06)
- **Backpropagation**: Karpathy's micrograd and "The spelled-out intro to neural networks"
- **Broadcasting**: NumPy official documentation, "NumPy Broadcasting" guide
- **Information theory**: Chapter 2 of Cover & Thomas "Elements of Information Theory"
- **Variational inference**: Blei et al. "Variational Inference: A Review for Statisticians" (arXiv 1601.00670)
