## Introduction

Most production systems that use machine learning for high-stakes decisions don't operate in fully automated mode. In anti-money laundering, fraud detection, content moderation, and medical triage, the standard architecture is a classifier that flags cases for human review. The assumption baked into this design is straightforward: humans catch what models miss, so adding review makes the system better.

This paper questions that assumption.

The problem is that human review costs money. Analysts have to be paid, cases take time to close, and compliance overhead adds up. False positives cost money too — they consume review capacity without catching anything real. False negatives carry their own costs, often much larger. When you lay these costs out explicitly, the question of whether to deploy human review, and how much, becomes an economic calculation — not just an accuracy question.

The machine learning literature has not treated it that way. HITL systems are evaluated almost universally on classification metrics: precision, recall, AUC. These metrics say nothing about whether the system-level cost went up or down. A HITL policy can improve precision on reviewed cases while simultaneously increasing total operational cost — and standard evaluation would report it as an improvement.

We study this problem through a cost-sensitive, decision-theoretic lens. The setting is AML-style transaction monitoring: a fixed trained classifier assigns risk scores to transactions, a threshold determines which get flagged, and a review policy determines which flagged cases go to a human analyst. We evaluate everything in terms of total expected cost — false positives, false negatives, and review costs combined — not accuracy.

The main finding is that naively applied HITL policies frequently increase total expected cost, even when human reviewers are more accurate than the model on reviewed cases. This is not a theoretical edge case. It happens across a wide range of realistic cost configurations. The gains from human error correction are simply outweighed by the cost of the review itself, especially when review is applied indiscriminately to cases where the model was already right.

We also show that optimizing the decision threshold alone — without any human review — often captures most of the available cost savings. The decision layer matters more than it is given credit for in practice.

A sensitivity analysis across 240 cost configurations adds a sharper finding: the critical variable governing HITL viability is human review cost, not false-negative severity. Whether a missed transaction costs $50 or $1,000, the regime pattern is the same. When review costs $20 or more per case, automation dominates across every cost combination we tested. This result substantially sharpens the regime boundaries and provides a concrete, operationalizable criterion for deployment decisions.

What makes this tractable as a study design is that we hold the classifier fixed throughout. We are not asking which model is best. We are asking how threshold selection and review allocation determine system-level cost, independent of model choice. The answer is: quite a lot.

## Contributions

This paper makes six contributions:

1. A cost-first evaluation framework for HITL decision systems that explicitly accounts for false-positive cost, false-negative cost, and human review cost.

2. A demonstration that decision-layer optimization — threshold selection and review allocation — can dominate model choice as a driver of system-level performance, without any retraining.

3. A formal negative result: naive HITL policies can increase total expected cost even when human reviewers outperform the model locally.

4. A characterization of three distinct cost regimes — automation-dominant, selective HITL, and HITL-degraded — and the conditions that determine which applies.

5. A failure taxonomy for HITL systems documenting the specific mechanisms by which human review degrades operational efficiency.

6. A sensitivity analysis across 240 cost configurations showing that human review cost — not false-negative severity — is the primary determinant of HITL viability, with automation dominating across all tested configurations when review costs $20 or more per case.
