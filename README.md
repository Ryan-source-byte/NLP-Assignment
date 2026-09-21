# Biomedical Abstract Classification Benchmark

A reproducible notebook study comparing domain-specific and self-trained word embeddings for five-class biomedical abstract classification.

The experiment keeps the downstream recurrent classifier fixed and changes the embedding source, making it easier to isolate the value of biomedical pretraining.

## Experiment design

- Dataset: 11,550 training abstracts and 2,888 test abstracts
- Task: five-class classification from a medical abstract
- Sequence policy: 166 tokens, chosen at the training-set 90th percentile
- Vocabulary: 32,303 tokens
- Embeddings: self-trained Word2Vec versus pretrained BioWordVec
- Model: masked recurrent neural network with a softmax classification head
- Metrics: accuracy and macro F1
- Analysis: t-SNE neighbourhood inspection and training/validation curves

## Results

| Embedding | Test accuracy | Macro F1 |
| --- | ---: | ---: |
| Self-trained Word2Vec | 0.4401 | 0.4421 |
| BioWordVec | **0.4640** | **0.4569** |

BioWordVec delivered the stronger held-out result under the same classifier. Both runs also showed a widening training-validation gap after the early epochs, so the main conclusion is not simply “use a larger model”: domain-aware representations helped, while regularisation and early stopping remain the clearest next improvements.

## What is in the notebook

1. Text cleaning, tokenisation and sequence-length analysis
2. Vocabulary construction and padding diagnostics
3. Self-trained Word2Vec and pretrained BioWordVec matrices
4. t-SNE comparison of biomedical semantic neighbourhoods
5. Two matched recurrent classifiers
6. Held-out evaluation and learning-curve analysis
7. An interactive inference form for test samples or custom abstracts

## Run

Open NLP_RyanGong.ipynb in Google Colab or Jupyter, then update the dataset and BioWordVec paths in the data-loading cells. The source datasets and pretrained embedding binary are not committed to this repository.

## Scope and limitations

This repository implements medical text classification, not clinical named-entity recognition and not a diagnostic system. Results come from one fixed split; stronger evidence would require repeated or cross-validated evaluation, per-class error analysis and modern transformer baselines.
