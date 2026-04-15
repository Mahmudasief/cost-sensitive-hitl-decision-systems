# Contributions and Failure Taxonomy

## What This Work Contributes

The core contribution is not a new model or a better algorithm. It is a reframing.

Most work on human-in-the-loop systems asks: how do we make human review more accurate? This paper asks a different question: given a fixed classifier and a fixed human reviewer, when does adding review actually reduce total operational cost — and when does it make things worse?

That shift in framing has six concrete outputs:

**1. A cost-first evaluation framework for HITL decision systems.** Rather than measuring precision, recall, or AUC, we evaluate every policy by its total expected cost: false positives, false negatives, and review costs combined. This is not the standard approach in the literature, and the difference matters — systems that look better on accuracy metrics can look worse on cost.

**2. Evidence that the decision layer dominates model choice.** We hold the classifier fixed throughout and show that threshold selection and review allocation alone determine whether a system performs well or badly under asymmetric costs. You can get larger performance differences by changing the decision policy than by swapping models — without retraining anything.

**3. A formal negative result.** Naive HITL policies — fixed review rates applied uniformly to flagged cases — frequently increase total expected cost, even when human reviewers are more accurate than the model on the cases they see. This is not a theoretical edge case. It happens across wide ranges of realistic cost configurations.

**4. A cost-regime map with a counterintuitive finding.** The conditions under which HITL helps versus hurts are not arbitrary. We identify three stable regimes — automation-dominant, selective HITL, and HITL-degraded — and characterize what determines which regime applies. The regime boundaries are driven almost entirely by human review cost, not false-negative severity. Sensitivity analysis across 240 cost configurations shows that when review costs $20 or more per case, automation dominates regardless of how large the false-negative cost is.

**5. Actionable deployment guidance for AML systems.** The findings translate directly into practice: optimize the decision threshold before deploying any human review, allocate review selectively to highest-risk cases, and treat review cost as a first-class input to system design — not an afterthought.

**6. A sensitivity analysis demonstrating robustness.** Results hold across 240 combinations of false-positive cost, false-negative cost, human review cost, and review rate. The qualitative finding is stable throughout: review cost is the gating variable for HITL viability, and the regime structure does not depend on specific cost assumptions.

---

## Failure Taxonomy for HITL Decision Systems

The following failure modes describe the specific mechanisms by which human review degrades system-level performance. Each is empirically grounded in the results of this study.

**Failure Mode 1: Cost-Blind Deployment**
Human review is introduced without explicitly modeling review cost or error asymmetry. The system flags cases, analysts review them, false positives go down — and total cost goes up. This is the most common failure mode in production AML systems. Reducing false positives is not the same as reducing cost.

**Failure Mode 2: Recall-Dominant Cost Regimes**
When false-negative costs are low relative to review costs, the expected benefit of catching an additional fraudulent transaction does not justify the cost of the review required to find it. HITL degrades performance in these regimes even when human reviewers are highly accurate.

**Failure Mode 3: Over-Broad Review Policies**
Fixed or high review rates applied uniformly across all flagged transactions waste human effort on cases where the model was already right. The analyst's time has a cost. Spending it on low-risk alerts erodes whatever efficiency gains were available from reviewing the high-risk ones.

**Failure Mode 4: Metric Illusion**
Standard ML metrics — precision, recall, F1, AUC — improve. Total expected cost increases. These outcomes are not contradictory; they measure different things. Systems can pass internal evaluation benchmarks while becoming economically worse. This failure mode is particularly dangerous because it is invisible to teams that do not model cost explicitly.

**Failure Mode 5: Human Superiority Fallacy**
Human reviewers outperform the model on the cases they see. Therefore HITL must help. This reasoning is wrong. Local accuracy improvements do not aggregate to global cost reductions when review itself is expensive and allocated without regard to impact. The reviewer being right more often is irrelevant if the cost of deploying the reviewer exceeds the value of the corrections.

---

## What This Taxonomy Is For

These failure modes are not hypothetical. They describe how real production HITL systems fail — quietly, in ways that accuracy metrics do not surface. The goal of formalizing them is to give practitioners and researchers a vocabulary for diagnosing when human review is working as intended and when it is not.

HITL is not inherently beneficial. It is a design choice with economic consequences. This taxonomy is a tool for making that choice deliberately.
