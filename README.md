# Decoding Barcelona's DNA

A data mining capstone analyzing 14 seasons of FC Barcelona's La Liga matches
using event-level data from the [StatsBomb open data repository](https://github.com/statsbomb/open-data).

**Author:** Robert
**Year:** 2026

---

## Overview

This project applies a full suite of data mining techniques to 449 Barcelona
La Liga matches (2004/05 – 2020/21) to identify patterns in playing style and
match outcomes:

- **Classification** — predict match outcome (Win / Draw / Loss) from 27 match-level features
- **Clustering** — discover tactical profiles using K-Means with PCA visualization
- **Association Rule Mining** — surface event patterns that co-occur with wins via Apriori

## Dataset

- **Source:** StatsBomb Open Data, competition_id = 11 (La Liga)
- **Scope:** 449 Barcelona matches across 14 seasons
- **Features:** 27 match-level features engineered from ~1.3M raw events
- **Class distribution:** 332 Wins / 74 Draws / 43 Losses

## Methods

| Technique | Approach |
|---|---|
| Classification | Decision Tree, Random Forest, Gradient Boosting, XGBoost, KNN |
| Hyperparameter tuning | 28-config grid search on KNN with stratified 5-fold CV |
| Evaluation | Macro-F1 (chosen over accuracy due to class imbalance) |
| Clustering | K-Means with elbow + silhouette selection; PCA for 2D projection |
| Association rules | Apriori on discretized features; filtered by lift |

## Key Results

- **Best classifier:** Gradient Boosting — test accuracy 0.767, macro-F1 0.501
- **Top predictors:** `key_passes` (0.102) and `barca_xg` (0.095) — chance creation outweighs chance quality
- **Clustering:** Silhouette selected k=2 — Barcelona's matches fall on a continuous dominance gradient rather than into discrete tactical modes
- **Association rules:** 1,351 frequent itemsets → 36,964 rules; top rules link high chance-creation patterns to wins (lift ≈ 1.88)

## Tech Stack

Python · Jupyter Notebook · pandas · NumPy · scikit-learn · XGBoost · mlxtend · matplotlib · seaborn


The notebook fetches data directly from StatsBomb's public GitHub repository on first run.

## Limitations & Future Work

- Single-team scope (StatsBomb open data has uniquely deep Barcelona coverage)
- Class imbalance unaddressed — future work should apply SMOTE or class weighting
- Era labels are subjective (manager-tenure proxies)

## License

Code released under the MIT License. StatsBomb data is subject to its own
[user agreement](https://github.com/statsbomb/open-data/blob/master/LICENSE.pdf).
