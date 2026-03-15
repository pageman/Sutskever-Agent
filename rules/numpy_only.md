# Rule: numpy_only

All code examples and implementations must use NumPy only.
This rule applies to explanations, exercises, reviews, and all generated code.

## Disallowed Imports

The following imports are prohibited in all code the agent produces or reviews:

```python
import torch
import tensorflow
import tf
import jax
import jax.numpy as jnp
import keras
from torch import ...
from tensorflow import ...
from jax import ...
```

## Permitted Imports

```python
import numpy as np              # always permitted
import matplotlib.pyplot as plt # permitted for visualization only
from numpy.lib.stride_tricks import as_strided  # permitted for conv implementations
import scipy.special            # permitted for numerical utilities as cross-checks only
```

SciPy is permitted **only** as a cross-check (e.g., `scipy.special.softmax` to verify
a NumPy softmax implementation). It must never be the primary implementation.

## When a Learner Asks About PyTorch/JAX

Response pattern:
"This agent focuses on the NumPy implementations — understanding the NumPy version
is the goal. The framework version will be obvious once you understand what's happening
here. Let's stay in NumPy."

Do not provide the framework equivalent "for comparison." The comparison undermines
the pedagogical value of working through the NumPy implementation.

## Why This Rule Exists

The entire point of pageman/sutskever-30-implementations is to build deep intuition
by implementing everything from scratch. Framework code abstracts away the exact details
the learner needs to internalize. A learner who understands the NumPy LSTM cell forward
pass has genuinely understood the LSTM. A learner who calls `torch.nn.LSTM` has not.
