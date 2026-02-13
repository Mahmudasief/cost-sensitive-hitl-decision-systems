## Cost-Sensitive Human-in-the-Loop Decision Systems Under Asymmetric Error Costs


## Overview

Human-in-the-loop (HITL) architectures are widely deployed in high-stakes decision systems—such as anti-money laundering (AML), fraud detection, content moderation, and medical triage—under the assumption that human review reliably improves outcomes.

This repository challenges that assumption.

We study HITL systems from a **cost-sensitive, decision-theoretic perspective** and show that **human review does not universally reduce total expected cost**. In many realistic cost regimes, naïvely applied HITL policies *increase* operational cost—even when human reviewers outperform automated models on specific error types.

**Main result** > Human review improves system-level performance **only under narrow cost regimes**; outside these regimes, HITL strictly degrades expected cost.



## Research Question

When does human review reduce total expected cost—and when does it increase it—in high-stakes decision systems with asymmetric error costs?


## Key Contributions

This repository provides:

 1. A cost-first evaluation framework for human-in-the-loop decision systems.
 2. A formal demonstration that decision policy and review allocation can dominate model choice, even without retraining.
 3. Empirical evidence that fixed-rate or indiscriminate HITL policies can degrade system-level performance.
 4. Identification of distinct cost regimes in which:
    - Fully automated decision-making is optimal
    - Selective HITL yields marginal gains
    - HITL strictly increases expected cost
 5. A formal negative result that serves as a counterexample to the assumption that adding human review is inherently beneficial.


## Methodological Scope

 - Problem setting: Binary classification with asymmetric false-positive and false-negative costs.
 - Application domain: AML-style transaction monitoring (used as a motivating example).
 - Classifier: Fixed, pre-trained probabilistic models (e.g., Random Forest, Logistic Regression).
 - Human review: Modeled as a costly intervention with imperfect correction probability.
 - Optimization target: Total expected operational cost (FP + FN + review costs).
 - Exclusions: No model retraining, active learning, or feedback loops (by design).

This deliberate scope isolates decision-layer effects and avoids confounding from model capacity or training dynamics.


## Cost Objective

We evaluate policies by minimizing total operational cost:
model_cost = fp_after * fp_cost + FN * fn_cost
human_review_cost = k * human_cost
total_cost = model_cost + human_review_cost
Where:
      fp_cost: fp_cost
      fn_cost: fn_cost
      human_cost: human_cost
      review_rate: review_rate
      human_reviews: k
      false_positives_after: fp_after
      false_negatives: FN
      

## Decision Pipeline

The evaluated decision process follows:

Model (probability scores)
↓
Decision Threshold (τ)
↓
Flagged Alerts
↓
Review Allocation Policy (π)
↓
Human Corrections
↓
Total Expected Operational Cost

This repository isolates decision-layer effects without retraining the underlying classifier.


## Main Findings (High-Level)

 - Cost-sensitive threshold optimization alone often yields larger gains than adding human review.
 - Human review can increase total expected cost when review cost is non-trivial or poorly allocated.
 - Selective HITL helps **only** when:
     False-negative cost is sufficiently high
     Review cost is sufficiently low
     Review is allocated to highest-impact cases
 - All regime transitions occur without retraining the model, highlighting the dominance of decision policy.


## Repository Structure

.
├── data/                   # Dataset documentation (raw data not committed)
├── notebooks/              # All experimental code, evaluation logic, and grid searches (Jupyter)
├── figures/                # Reserved for optional generated plots (not committed by default)
├── results/                # Reserved for serialized outputs if needed (results reported in markdown)
├── src/                    # Reserved for future modularization (current implementation is notebook-based)
├── ABSTRACT.md             # Paper abstract
├── INTRODUCTION.md         # Motivation and background
├── METHODS.md              # Formal problem formulation and cost model
├── RESULTS.md              # Empirical findings and regime analysis
├── RESULTS_NUMBERS.md      # Quantitative results only (no interpretation)
├── DISCUSSION.md           # Interpretation and implications
├── THREATS_AND_VALIDITY.md # Limitations and anticipated reviewer objections
├── PAPER_CLAIM.md          # Core research claims and contributions
└── README.md               # Repository overview (this file)
All experiments and analyses are implemented in Jupyter notebooks to emphasize transparency and reproducibility of decision-layer evaluation.


**Limitation:** This analysis assumes static models and fixed human correction rates; dynamic retraining, learning effects, and capacity constraints are not modeled.


## Reproducibility

This repository follows a notebook-first research workflow.

### Environment
All experiments were run using Python ≥3.9.  
Minimal dependencies are listed in `requirements.txt`.

To install:

```bash
pip install -r requirements.txt
```

### Execution Order
Empirical analyses are executed in the following order:

1. Notebooks in `notebooks/` for data loading, cost modeling, and evaluation
2. Results are summarized and reported in:
   - `RESULTS.md`
   - `RESULTS_NUMBERS.md`

No model retraining or stochastic pipelines are used; results are deterministic given the dataset and parameters.


## Why This Matters

Most HITL systems are evaluated using accuracy-centric metrics, which can obscure real operational trade-offs. This work shows that:

 - Local accuracy improvements ≠ global system improvements.
 - Human review is an economic intervention, not a guaranteed safeguard.
 - Cost modeling must precede deployment decisions in high-stakes systems.

These findings explain why many production HITL systems suffer from investigator overload despite continuous investment in manual review.


## Intended Audience

 - PhD admissions committees
 - ML + OR researchers
 - AML / risk analytics practitioners
 - Reviewers evaluating cost-sensitive ML systems
 - Policymakers and system designers


## Citation

If you reference this work, please cite the repository and accompanying manuscript materials.
