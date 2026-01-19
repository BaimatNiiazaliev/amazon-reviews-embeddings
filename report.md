# Technical Report: Sentiment Classification with Precomputed Embeddings

## Overview
This project studies sentiment classification of Amazon product reviews using
precomputed text representations. The goal is to compare how different embedding
spaces influence downstream classification performance and representation
structure, while keeping the modeling pipeline simple and controlled.

The analysis focuses on three feature types:
- Bag-of-Words (BoW)
- BERT embeddings
- OpenAI embeddings

All embeddings are provided with a fixed train/test split and are treated as
inputs to downstream models.

---

## Data
The dataset consists of Amazon customer reviews labeled as positive or negative
based on star ratings. Three precomputed representations are provided:
- BoW feature vectors
- BERT embeddings
- OpenAI embeddings

Each embedding corresponds to the same set of reviews and shares a common
train/test split, enabling direct comparison across representations.

Raw text preprocessing and embedding generation are out of scope for this project.

---

## Methods

### Dimensionality Reduction
To analyze the geometric structure of the embedding spaces, dimensionality
reduction techniques were applied to the training data:
- **PCA** was used to project embeddings into two dimensions for visualization
- **UMAP** was explored as a nonlinear alternative where applicable

These projections serve as diagnostic tools rather than performance measures.

---

### Classification Model
For all representations, sentiment classification was performed using
**Multinomial Naive Bayes**.

- A baseline model was trained using a fixed smoothing parameter (alpha = 4)
- Hyperparameter tuning was performed via cross-validation to select the optimal
  alpha value for each embedding type
- Final models were evaluated on a held-out test set

For dense embeddings (BERT and OpenAI), feature scaling was applied as required
to ensure compatibility with the classifier.

---

## Evaluation
Model performance was evaluated using test error rates and confusion matrices.
In addition, qualitative inspection of misclassified examples was used to
identify systematic error patterns.

To assess robustness, models were also trained on progressively smaller subsets
of the training data, allowing comparison of performance as a function of sample
size across embedding methods.

---

## Results and Observations
Key observations from the experiments include:
- Simple BoW representations provide strong baseline performance
- Dense embeddings exhibit improved semantic structure in low-dimensional
  projections
- OpenAI embeddings show particularly coherent class separation in visualization
- Embedding-based models are more robust under reduced training data scenarios
- Zero-shot classification using OpenAI embeddings is feasible but less accurate
  than supervised approaches

These results highlight the tradeoff between simplicity, semantic richness, and
data efficiency.

---
## Results Summary

- BoW + Naive Bayes: test error ≈ 14%
- BERT + Naive Bayes: test error ≈ 21%
- OpenAI embeddings + Naive Bayes: test error ≈ 4%
- OpenAI zero-shot baseline: test error ≈ 2.8–3.3%

Detailed confusion matrices and robustness analyses are provided in the notebook.

---
## Discussion
This project illustrates that improvements in representation quality do not
automatically translate into proportional gains in classification accuracy.
While dense embeddings offer advantages in robustness and semantic structure,
they also introduce additional complexity and dependency considerations.

The results reinforce the importance of establishing strong baselines and
evaluating representation choices in the context of downstream constraints.

---

## Limitations and Future Work
- Labels derived from star ratings introduce noise and ambiguity
- Only a single classifier family was explored
- Computational cost and latency were not explicitly measured

Future extensions could include alternative classifiers, calibration analysis,
and evaluation under distributional shift.

---

## Conclusion
By holding the modeling pipeline constant and varying only the feature
representation, this project provides a controlled comparison of sparse and
dense embeddings for sentiment classification. The findings emphasize practical
tradeoffs that are directly relevant to real-world machine learning systems.
