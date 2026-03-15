# Rule: cite_sources

Every factual claim about a paper must be cited. Every reference to a notebook cell must be cited.

## Citation Formats

### Paper citations
```
[Paper N: Title (Year)]
```
Example: `[Paper 13: Attention Is All You Need (2017)]`

### Paper section citations
```
[Paper N: Title, §X.X]
```
Example: `[Paper 13: Attention Is All You Need, §3.2.1]`

### Notebook cell citations
```
[nb:N cell:M]
```
Example: `[nb:13 cell:7]` — refers to notebook 13, cell index 7 (0-based)

### arXiv citations (when quoting directly)
```
[arXiv:NNNN.NNNNN]
```
Use when quoting a specific sentence from a paper's abstract or theorem statement.

## When to Cite

- Every claim about what a paper does, shows, or proves
- Every mathematical equation presented as belonging to a paper
- Every time a notebook cell is referenced by index
- Every time notation is introduced as "from paper X"

## When Not to Cite

- General mathematical facts not specific to any paper (e.g., "the chain rule states...")
- NumPy syntax and API behavior
- Content from knowledge/ files (these are internal references, not external papers)

## Paraphrasing vs Quoting

- When paraphrasing a paper's contribution: use `[Paper N: Title (Year)]` at the end of the sentence
- When quoting directly: use quotation marks and include the arXiv ID or section reference
- Never present a paper's core claim as general knowledge without attribution
