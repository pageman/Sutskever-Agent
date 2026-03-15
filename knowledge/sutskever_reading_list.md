# Sutskever Reading List — 30 Papers

Source: pageman/sutskever-30-implementations
All papers implemented in pure NumPy.

---

## Learning Tracks

### Beginner Track (start here if new to deep learning)
Recommended order: 7 → 10 → 11 → 22 → 26 → 2 → 3

### Intermediate Track (comfortable with backprop, new to advanced architectures)
Recommended order: 2 → 3 → 4 → 6 → 13 → 14 → 16 → 18 → 20 → 22 → 26 → 28

### Advanced Track (familiar with most architectures, want depth)
Recommended order: 5 → 8 → 9 → 12 → 17 → 19 → 21 → 23 → 24 → 25 → 27 → 29 → 30

### Theory Track (mathematical foundations, information theory, complexity)
Recommended order: 5 → 23 → 24 → 25 → 1 → 8 → 19

---

## Thematic Clusters

### Cluster 1: Sequence Models and Memory
Papers: 2, 3, 4, 18, 20, 29, 30
Theme: How to model sequences, encode long-range dependencies, and add persistent memory.

### Cluster 2: Attention and Transformers
Papers: 6, 13, 14, 16, 28
Theme: Moving from fixed-size context vectors to dynamic, query-based attention over full sequences.

### Cluster 3: Vision and Convolutional Architectures
Papers: 7, 10, 11, 15, 26
Theme: Hierarchical feature extraction from pixels to semantic representations.

### Cluster 4: Information Theory, Compression, and Foundations
Papers: 1, 5, 8, 9, 17, 19, 23, 24, 25
Theme: The theoretical underpinnings — what is learning, what is compression, what are the limits?

---

## All 30 Papers

| # | Title | Year | Cluster | Track | Est. Hours |
|---|-------|------|---------|-------|-----------|
| 1 | The Annotated Transformer | 2018 | Theory | Theory | 4h |
| 2 | Generating Sequences With Recurrent Neural Networks (Char-RNN) | 2013 | Sequence | Intermediate | 3h |
| 3 | Sequence to Sequence Learning with Neural Networks | 2014 | Sequence | Intermediate | 4h |
| 4 | Neural Turing Machines | 2014 | Sequence | Intermediate | 8h |
| 5 | A Tutorial Introduction to the Minimum Description Length Principle | 2004 | Theory | Theory | 6h |
| 6 | Pointer Networks | 2015 | Attention | Intermediate | 4h |
| 7 | ImageNet Classification with Deep CNNs (AlexNet) | 2012 | Vision | Beginner | 4h |
| 8 | Kolmogorov Complexity and Algorithmic Randomness | 2019 | Theory | Advanced | 8h |
| 9 | Hutter Prize / Large Text Compression | 2006 | Theory | Advanced | 4h |
| 10 | Gradient-Based Learning Applied to Document Recognition (LeNet) | 1998 | Vision | Beginner | 3h |
| 11 | Very Deep Convolutional Networks (VGGNet) | 2014 | Vision | Beginner | 3h |
| 12 | Dropout: A Simple Way to Prevent Overfitting | 2014 | Advanced | Advanced | 2h |
| 13 | Attention Is All You Need (Transformer) | 2017 | Attention | Intermediate | 6h |
| 14 | Neural Machine Translation by Jointly Learning to Align and Translate | 2015 | Attention | Intermediate | 5h |
| 15 | Deep Residual Learning for Image Recognition (ResNet) | 2016 | Vision | Intermediate | 4h |
| 16 | Language Models are Unsupervised Multitask Learners (GPT-2) | 2019 | Attention | Intermediate | 6h |
| 17 | Auto-Encoding Variational Bayes (VAE) | 2013 | Theory | Advanced | 6h |
| 18 | Relational Recurrent Neural Networks | 2018 | Sequence | Advanced | 12h |
| 19 | The First Law of Complexodynamics | 2011 | Theory | Theory | 3h |
| 20 | Memory Networks | 2014 | Sequence | Intermediate | 4h |
| 21 | Connectionist Temporal Classification (CTC) | 2006 | Advanced | Advanced | 8h |
| 22 | Recurrent Neural Network Regularization | 2014 | Sequence | Beginner | 2h |
| 23 | Quantifying the Rise and Fall of Complexity in Closed Systems | 2014 | Theory | Theory | 4h |
| 24 | A Mathematical Framework for Transformer Circuits | 2021 | Theory | Theory | 8h |
| 25 | In-context Learning and Induction Heads | 2022 | Theory | Theory | 6h |
| 26 | Densely Connected Convolutional Networks (DenseNet) | 2017 | Vision | Intermediate | 4h |
| 27 | Proximal Policy Optimization Algorithms (PPO) | 2017 | Advanced | Advanced | 6h |
| 28 | Graph Attention Networks (GAT) | 2018 | Attention | Intermediate | 5h |
| 29 | Scaling Laws for Neural Language Models | 2020 | Sequence | Advanced | 4h |
| 30 | An Image is Worth 16x16 Words (ViT) | 2020 | Attention | Advanced | 6h |

---

## Difficulty Labels

- **Beginner**: No prior deep learning implementation experience required
- **Intermediate**: Comfortable with backprop and NumPy; has read 1-2 papers before
- **Advanced**: Familiar with most architectures; can read math-heavy papers directly
- **Theory**: Requires comfort with information theory, complexity theory, or mechanistic interpretability
