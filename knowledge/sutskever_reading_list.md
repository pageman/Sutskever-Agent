# Sutskever Reading List — 30 Papers

Source: pageman/sutskever-30-implementations
All papers implemented in pure NumPy.
Organized into four sections matching the source repository's structure.

---

## Repository Sections

The source repo organizes the 30 notebooks into four sections:

| Section | Papers | Theme |
|---------|--------|-------|
| Foundational Concepts | 1–5 | Complexity, RNNs, LSTMs, regularization, description length |
| Architectures & Mechanisms | 6–15 | Pointer networks, CNNs, attention, residual learning |
| Advanced Topics | 16–22 | Relational reasoning, VAE, NTM, CTC, scaling laws |
| Theory & Meta-Learning | 23–30 | MDL, Kolmogorov, intelligence, retrieval, long context |

---

## Learning Tracks

### Beginner Track (start here if new to deep learning)
Recommended order: 2 → 3 → 4 → 7 → 26 → 6 → 8

### Intermediate Track (comfortable with backprop, new to advanced architectures)
Recommended order: 4 → 6 → 8 → 14 → 13 → 10 → 11 → 15 → 16 → 18 → 20 → 22 → 27 → 28 → 29 → 30

### Advanced Track (familiar with most architectures, want depth)
Recommended order: 1 → 5 → 17 → 19 → 20 → 21 → 23 → 24 → 25

### Theory Track (mathematical foundations, information theory, complexity)
Recommended order: 1 → 5 → 19 → 23 → 24 → 25

---

## Thematic Clusters

### Cluster 1: Sequence Models and Memory
Papers: 2, 3, 4, 8, 18, 20
Theme: How to model sequences, encode long-range dependencies, and add persistent memory.

### Cluster 2: Attention and Transformers
Papers: 6, 13, 14, 16
Theme: Moving from fixed-size context vectors to dynamic, query-based attention over full sequences.

### Cluster 3: Vision and Convolutional Architectures
Papers: 7, 10, 11, 15, 26
Theme: Hierarchical feature extraction from pixels to semantic representations.

### Cluster 4: Information Theory, Compression, and Foundations
Papers: 1, 5, 19, 23, 24, 25
Theme: The theoretical underpinnings — what is learning, what is compression, what are the limits?

### Cluster 5: Scaling and Infrastructure
Papers: 9, 22, 27
Theme: How do systems scale? Pipeline parallelism, power laws, and prediction efficiency.

### Cluster 6: Retrieval and Long Context
Papers: 28, 29, 30
Theme: Augmenting LLMs with external knowledge and understanding how context length affects recall.

---

## All 30 Papers

### Section 1: Foundational Concepts

| # | Title | Year | Cluster | Track | Est. Hours |
|---|-------|------|---------|-------|-----------|
| 1 | The First Law of Complexodynamics | 2011 | Info Theory | Theory | 3h |
| 2 | The Unreasonable Effectiveness of Recurrent Neural Networks | 2015 | Sequence | Beginner | 2h |
| 3 | Understanding LSTM Networks | 2015 | Sequence | Beginner | 2h |
| 4 | Recurrent Neural Network Regularization | 2014 | Sequence | Beginner | 2h |
| 5 | Keeping Neural Networks Simple (MDL of Weights) | 1993 | Info Theory | Theory | 5h |

### Section 2: Architectures & Mechanisms

| # | Title | Year | Cluster | Track | Est. Hours |
|---|-------|------|---------|-------|-----------|
| 6 | Pointer Networks | 2015 | Attention | Intermediate | 4h |
| 7 | ImageNet Classification with Deep CNNs (AlexNet) | 2012 | Vision | Beginner | 4h |
| 8 | Order Matters: Sequence to Sequence for Sets | 2016 | Sequence | Intermediate | 4h |
| 9 | GPipe: Easy Scaling with Micro-Batch Pipeline Parallelism | 2019 | Scaling | Intermediate | 3h |
| 10 | Deep Residual Learning for Image Recognition (ResNet) | 2016 | Vision | Intermediate | 4h |
| 11 | Multi-Scale Context Aggregation by Dilated Convolutions | 2016 | Vision | Intermediate | 3h |
| 12 | Neural Message Passing for Quantum Chemistry | 2017 | Graphs | Intermediate | 4h |
| 13 | Attention Is All You Need (Transformer) | 2017 | Attention | Intermediate | 6h |
| 14 | Neural Machine Translation by Jointly Learning to Align and Translate | 2015 | Attention | Intermediate | 5h |
| 15 | Identity Mappings in Deep Residual Networks (ResNet v2) | 2016 | Vision | Intermediate | 3h |

### Section 3: Advanced Topics

| # | Title | Year | Cluster | Track | Est. Hours |
|---|-------|------|---------|-------|-----------|
| 16 | A Simple Neural Network Module for Relational Reasoning | 2017 | Attention | Intermediate | 4h |
| 17 | Variational Lossy Autoencoder | 2017 | Generative | Advanced | 6h |
| 18 | Relational Recurrent Neural Networks | 2018 | Sequence | Advanced | 12h |
| 19 | The Coffee Automaton | 2014 | Info Theory | Theory | 3h |
| 20 | Neural Turing Machines | 2014 | Sequence | Advanced | 8h |
| 21 | Deep Speech 2: End-to-End Speech Recognition | 2016 | Speech | Advanced | 8h |
| 22 | Scaling Laws for Neural Language Models | 2020 | Scaling | Intermediate | 4h |

### Section 4: Theory & Meta-Learning

| # | Title | Year | Cluster | Track | Est. Hours |
|---|-------|------|---------|-------|-----------|
| 23 | A Tutorial Introduction to the MDL Principle | 2004 | Info Theory | Theory | 6h |
| 24 | Machine Super Intelligence | 2008 | Info Theory | Theory | 5h |
| 25 | Kolmogorov Complexity and Algorithmic Randomness | 2019 | Info Theory | Advanced | 8h |
| 26 | CS231n: CNNs for Visual Recognition | 2022 | Vision | Beginner | 4h |
| 27 | Better & Faster LLMs via Multi-token Prediction | 2024 | Scaling | Intermediate | 4h |
| 28 | Dense Passage Retrieval for Open-Domain QA | 2020 | Retrieval | Intermediate | 4h |
| 29 | Retrieval-Augmented Generation | 2020 | Retrieval | Intermediate | 4h |
| 30 | Lost in the Middle: How LMs Use Long Contexts | 2023 | Retrieval | Intermediate | 3h |

---

## Difficulty Labels

- **Beginner**: No prior deep learning implementation experience required
- **Intermediate**: Comfortable with backprop and NumPy; has read 1-2 papers before
- **Advanced**: Familiar with most architectures; can read math-heavy papers directly
- **Theory**: Requires comfort with information theory, complexity theory, or algorithmic probability

---

## Total Estimated Time

| Track | Papers | Hours |
|-------|--------|-------|
| Beginner | 2, 3, 4, 7, 26 | ~14h |
| Intermediate | 6, 8, 9, 10, 11, 12, 13, 14, 15, 16, 22, 27, 28, 29, 30 | ~58h |
| Advanced | 17, 18, 20, 21, 25 | ~42h |
| Theory | 1, 5, 19, 23, 24 | ~22h |
| **All 30** | | **~136h** |
