## Refine abstract to align with cost-sensitive HITL framing and negativ…


## Overview

Human-in-the-loop (HITL) architectures are widely deployed in high-stakes decision systems such as anti-money laundering (AML), fraud detection, content moderation, and medical triage. In these systems, automated classifiers are augmented with manual review under the assumption that human intervention reliably improves outcomes.

This project challenges that assumption.

We study HITL decision systems from a cost-sensitive decision-theoretic perspective, evaluating system performance using total expected operational cost rather than classification accuracy or AUC. We show that naïvely applied human review policies can increase total expected cost, even when human reviewers outperform automated models on specific error types such as false positives.

The central finding is that human intervention is not universally beneficial. Its effectiveness depends critically on error-cost asymmetry, review cost, and review allocation strategy.


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
 5. A negative result that serves as a counterexample to the assumption that adding human review is inherently beneficial.


## Methodological Scope

 - Problem setting: Binary classification with asymmetric false-positive and false-negative costs.
 - Application domain: AML-style transaction monitoring (used as a motivating example).
 - Classifier: Fixed, pre-trained probabilistic models (e.g., Random Forest, Logistic Regression).
 - Human review: Modeled as an optional intervention with explicit cost and imperfect correction probability.
 - Optimization target: Total expected operational cost (FP + FN + review costs).
 - Exclusions: No model retraining, active learning, or feedback loops (by design).

This deliberate scope isolates decision-layer effects and avoids confounding from model capacity or training dynamics.


## Repository Structure

.
├── data/                  # AML-style datasets
├── notebooks/             # Experimental evaluation and grid search
├── src/                   # Cost modeling and policy evaluation code
├── figures/               # Plots and visualizations
├── results/               # Saved outputs
├── ABSTRACT.md            # Paper abstract
├── INTRODUCTION.md        # Motivation and background
├── METHODS.md             # Formal problem formulation and cost model
├── RESULTS.md             # Empirical findings and regime analysis
├── RESULTS_NUMBERS.md     # Quantitative results only (no interpretation)
├── DISCUSSION.md          # Interpretation and implications
├── THREATS_AND_VALIDITY.md# Limitations and reviewer objections
├── PAPER_CLAIM.md         # Core claims and contributions
└── README.md              # This file


## Main Findings (High-Level)

 - Cost-sensitive threshold optimization alone often yields larger gains than adding human review.
 - Human review can increase total expected cost when review cost is non-trivial or poorly allocated.
 - Selective HITL helps only under narrow and explicit economic conditions.
 - All regime transitions occur without retraining the model, highlighting the dominance of decision policy.


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


## Status

This repository represents a research-ready artifact suitable for:
 - PhD applications
 - Methodological papers
 - Workshop or conference submission
 - National Interest Waiver (NIW) evidence


## Citation

If you reference this work, please cite the repository and accompanying manuscript materials.
