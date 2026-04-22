# Cost-Sensitive Human-in-the-Loop Decision Systems Under Asymmetric Error Costs

## Overview

Human-in-the-loop (HITL) architectures are widely deployed in high-stakes decision systems — such as anti-money laundering (AML), fraud detection, content moderation, and medical triage — under the assumption that human review reliably improves outcomes.

This repository challenges that assumption.

We study HITL systems from a **cost-sensitive, decision-theoretic perspective** and show that **human review does not universally reduce total expected cost**. In many realistic cost regimes, naively applied HITL policies increase operational cost — even when human reviewers outperform automated models on specific error types.

**Main result:** Human review improves system-level performance only under narrow cost regimes; outside these regimes, HITL strictly degrades expected cost.

## Research Question

When does human review reduce total expected cost — and when does it increase it — in high-stakes decision systems with asymmetric error costs?

## Key Contributions

1. A cost-first evaluation framework for human-in-the-loop decision systems.
2. A formal demonstration that decision policy and review allocation can dominate model choice, even without retraining.
3. Empirical evidence that fixed-rate or indiscriminate HITL policies can degrade system-level performance.
4. Identification of distinct cost regimes in which fully automated decision-making is optimal, selective HITL yields marginal gains, or HITL strictly increases expected cost.
5. A formal negative result that serves as a counterexample to the assumption that adding human review is inherently beneficial.
6. A formal failure taxonomy identifying five mechanisms by which HITL intervention degrades operational efficiency, documented in CONTRIBUTIONS_AND_FAILURES.md.
7. A sensitivity analysis across 240 cost configurations showing that human review cost — not false-negative severity — is the primary determinant of HITL viability, documented in SENSITIVITY_ANALYSIS.md.

## Methodological Scope

* Problem setting: Binary classification with asymmetric false-positive and false-negative costs.
* Application domain: AML-style transaction monitoring (used as a motivating example).
* Classifier: Fixed, pre-trained probabilistic models (e.g., Random Forest, Logistic Regression).
* Human review: Modeled as a costly intervention with imperfect correction probability.
* Optimization target: Total expected operational cost (FP + FN + review costs).
* Exclusions: No model retraining, active learning, or feedback loops (by design).

This deliberate scope isolates decision-layer effects and avoids confounding from model capacity or training dynamics.

## Cost Objective

We evaluate policies by minimizing total operational cost:

```
model_cost        = fp_after * fp_cost + FN * fn_cost
human_review_cost = k * human_cost
total_cost        = model_cost + human_review_cost
```

Where:

* `fp_cost` : cost of a false positive
* `fn_cost` : cost of a false negative
* `human_cost` : cost per reviewed case
* `review_rate` : fraction of flagged alerts reviewed
* `k` : number of reviewed cases
* `fp_after` : false positives after review
* `FN` : false negatives

## Decision Pipeline

The evaluated decision process follows:

1. Model (probability scores)
2. Decision Threshold (τ)
3. Flagged Alerts
4. Review Allocation Policy (π)
5. Human Corrections
6. Total Expected Operational Cost

This repository isolates decision-layer effects without retraining the underlying classifier.

## Main Findings (High-Level)

* Cost-sensitive threshold optimization alone often yields larger gains than adding human review.
* Human review can increase total expected cost when review cost is non-trivial or poorly allocated.
* Selective HITL helps only when false-negative cost is sufficiently high, review cost is sufficiently low, and review is allocated to highest-impact cases.
* All regime transitions occur without retraining the model, highlighting the dominance of decision policy.
* Sensitivity analysis across 240 cost configurations shows that human review cost — not false-negative severity — is the primary determinant of HITL viability. When review costs $20 or more per case, automation dominates across all tested parameter combinations.

## Repository Structure

```
├── data/                          # Dataset documentation (raw data not committed)
├── notebooks/
│   ├── 01_eda.ipynb               # Exploratory data analysis and class imbalance visualization
│   └── 02_baseline_models.ipynb   # Cost-sensitive thresholding, HITL policy grid search, sensitivity analysis
├── figures/                       # Cost-vs-threshold plots (RF, LR), EDA charts, HITL regime heatmap
├── results/                       # Reserved for serialized outputs
├── src/                           # Reserved for future modularization
├── ABSTRACT.md                    # Paper abstract
├── INTRODUCTION.md                # Motivation and background
├── METHODS.md                     # Formal problem formulation and cost model
├── RESULTS.md                     # Empirical findings and regime analysis
├── RESULTS_NUMBERS.md             # Quantitative results only (no interpretation)
├── DISCUSSION.md                  # Interpretation and implications
├── THREATS_AND_VALIDITY.md        # Limitations and anticipated reviewer objections
├── SENSITIVITY_ANALYSIS.md        # Sensitivity analysis across 240 cost configurations
├── CONTRIBUTIONS_AND_FAILURES.md  # Failure taxonomy for HITL decision systems
├── PAPER_CLAIM.md                 # Core research claims (internal scaffolding)
└── README.md                      # Repository overview (this file)
```

**Limitation:** This analysis assumes static models and fixed human correction rates; dynamic retraining, learning effects, and capacity constraints are not modeled.

## Reproducibility

### Environment

All experiments were run using Python ≥3.9. Minimal dependencies are listed in `requirements.txt`.

```
pip install -r requirements.txt
```

### Execution Order

1. `notebooks/01_eda.ipynb` — Exploratory data analysis: class imbalance, transaction amount distribution, fraud rate by amount, and feature correlations.
2. `notebooks/02_baseline_models.ipynb` — Baseline model training, cost-sensitive threshold optimization, HITL policy evaluation across cost regimes, and sensitivity analysis.

Results are summarized in `METHODS.md`, `RESULTS.md`, `RESULTS_NUMBERS.md`, and `SENSITIVITY_ANALYSIS.md`.

No model retraining or stochastic pipelines are used; results are deterministic given the dataset and parameters.

## Why This Matters

Most HITL systems are evaluated using accuracy-centric metrics, which can obscure real operational trade-offs. This work shows that:

* Local accuracy improvements do not equal global system improvements.
* Human review is an economic intervention, not a guaranteed safeguard.
* Cost modeling must precede deployment decisions in high-stakes systems.
* Review cost — not error severity — is the primary gating factor for HITL viability.

These findings explain why many production HITL systems suffer from investigator overload despite continuous investment in manual review.

## Intended Audience

* PhD admissions committees
* ML + OR researchers
* AML / risk analytics practitioners
* Reviewers evaluating cost-sensitive ML systems
* Policymakers and system designers

## Citation

Mahmud, M. A. (2026). Cost-Sensitive Human-in-the-Loop Decision Systems Under Asymmetric Error Costs. SSRN Working Paper 6592940.
https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6592940
