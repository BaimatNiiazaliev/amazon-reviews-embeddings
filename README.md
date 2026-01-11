# Amazon Reviews – Sentiment Classification with Precomputed Embeddings

This project evaluates sentiment classification on Amazon product reviews using
precomputed text representations, comparing sparse features (Bag-of-Words)
with dense semantic embeddings (BERT and OpenAI).

The focus is on **modeling and engineering tradeoffs at the representation level**,
rather than raw text preprocessing.

---

## Problem
User reviews contain rich information about product quality and customer sentiment.
In many real-world machine learning pipelines, practitioners work with
**precomputed features or embeddings** due to cost, privacy, or architectural constraints.

The goal of this project is to analyze how different text representations affect
classification performance, robustness, and practical usability under a controlled setup.

---

## Data
The project uses a prepared Amazon Reviews dataset with:
- Precomputed Bag-of-Words feature matrices
- Precomputed BERT embeddings
- Precomputed OpenAI embeddings

Each representation is provided with a predefined train/test split,
enabling consistent and fair comparison across models.

---

## Approach
- Load and validate precomputed feature matrices and embeddings
- Train downstream classifiers, with a focus on **Multinomial Naive Bayes**
- Tune smoothing parameters (**alpha**) via cross-validation
- Evaluate generalization performance on a held-out test set
- Compare performance across feature representations
- Analyze confusion matrices and systematic error patterns
- Use **PCA** as a diagnostic tool to visualize representation structure
- Optionally explore nonlinear projections (e.g., **UMAP**) for qualitative analysis

---

## Repository structure
<pre>
amazon-reviews-embeddings/
├── notebooks/        # Experiments and analysis using precomputed features
├── src/              # Modeling and evaluation code
├── report.md         # Technical report and findings
├── results/          # Evaluation artifacts and figures
├── README.md
└── requirements.txt
</pre>

## Status
This repository is under active development.
Experiments and analysis are being added incrementally.

---

## Notes
- Raw text preprocessing is out of scope for this project.
- Large datasets and embedding files are not stored in the repository.
- API keys and credentials are not committed.
- This project is based on a structured academic assignment and adapted for portfolio presentation.
