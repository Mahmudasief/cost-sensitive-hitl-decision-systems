## Cost-Sensitive Human-in-the-Loop Decision Systems Under Asymmetric Error Costs


## Overview


Human-in-the-loop (HITL) architectures are widely deployed in high-stakes decision systems—such as anti-money laundering (AML), fraud detection, content moderation, and medical triage—under the assumption that human review reliably improves outcomes.


This repository challenges that assumption.


We study HITL systems from a **cost-sensitive, decision-theoretic perspective** and show that **human review does not universally reduce total expected cost**. In many realistic cost regimes, naïvely applied HITL policies increase operational cost—even when human reviewers outperform automated models on specific error types.


**Main result:** Human review improves system-level performance only under narrow cost regimes; outside these regimes, HITL strictly degrades expected cost.


## Research Question


When does human review reduce total expected cost—and when does it increase it—in high-stakes decision systems with asymmetric error costs?


## Key Contributions


This repository provides:


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
