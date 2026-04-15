# Results and Empirical Regimes

## Overview

We evaluate automated and human-in-the-loop (HITL) decision policies across a wide range of cost regimes to understand when human intervention reduces total expected operational cost — and when it does not. All results are reported in terms of total expected cost, not classification accuracy or AUC. The underlying classifier is held fixed throughout.

---

## Baseline: Automated Decision-Making

Across all cost regimes, we first identify the optimal automated threshold that minimizes expected cost without any human review. This automated baseline serves as the reference point against which all HITL policies are compared.

In several regimes, especially those with moderate false-negative costs and non-trivial review cost, the automated baseline achieves the lowest expected cost among all evaluated policies. Importantly, none of the top-ranked HITL configurations outperform the automated baseline under the primary cost setting. All HITL policies that beat the baseline occur outside the primary cost regime and require specific cost asymmetries to do so.

---

## Effect of Cost-Sensitive Thresholding

Optimizing the decision threshold alone yields substantial reductions in false positives and total cost relative to standard accuracy-optimized thresholds. In many regimes, threshold optimization without human review captures the majority of achievable cost savings — highlighting the importance of decision-layer optimization before considering HITL at all.

---

## Naive HITL Increases Total Cost

Naively applied HITL policies — fixed-rate review of flagged transactions regardless of risk score — increase total expected cost, even when human reviewers outperform the model on false positives.

The mechanism is straightforward: review costs money. When the cost of reviewing an alert exceeds the expected savings from correcting the errors found, the system loses money on every review. This is compounded when review is allocated to low-risk cases the model already handled correctly — human effort is spent confirming right decisions rather than catching wrong ones.

This directly contradicts the assumption that adding human review is inherently beneficial.

---

## Selective HITL and Marginal Gains

Selective review strategies that concentrate human effort on the highest-risk flagged cases can outperform fixed-rate HITL policies. However, even selective HITL does not beat the optimal automated baseline under the primary cost configuration. Gains are marginal and only emerge when false-negative costs are high, review costs are low, and review capacity is tightly constrained. Outside these conditions, automation dominates.

---

## Empirical Cost Regimes

Three distinct regimes emerge from the results:

**Regime I — Automation Dominant**
Review costs are high relative to error costs. The optimal policy is fully automated decision-making. HITL strictly degrades performance in this regime.

**Regime II — Selective HITL Viable**
False-negative costs are high, review costs are low, and review is concentrated on the highest-risk cases. HITL yields modest cost reductions. Improvements occur away from the global cost minimum and do not dominate the optimal automated policy overall.

**Regime III — HITL Failure**
Review is applied broadly or indiscriminately. Local accuracy improves on reviewed cases. Total expected cost increases due to operational overhead. This is the most common failure mode in production HITL systems.

These regimes are stable across wide ranges of reviewer accuracy and model calibration.

---

## Decision Policy Dominates Model Choice

All observed regime transitions occur without retraining the model. Threshold selection and review allocation alone determine which regime the system falls into. This means decision policy can dominate model choice as a driver of system-level performance under asymmetric error costs — a result with direct implications for how production AML systems should be designed and evaluated.

---

## Sensitivity Analysis

The primary results are reported under a specific cost configuration (FP=$5, FN=$500, review=$20). To test robustness, we evaluated 240 cost combinations spanning FP costs of $1–$20, FN costs of $50–$1,000, human review costs of $5–$50, and review rates of 5%–20%.

Of the 240 configurations, 45 (18.75%) show HITL beating the automated baseline. The other 195 (81.25%) show HITL increasing total cost.

The most striking result from the sensitivity analysis is that false-negative cost has almost no effect on the outcome. The regime pattern is determined almost entirely by human review cost:

- At $5/review: HITL beats baseline in 50% of configurations
- At $10/review: HITL beats baseline in 25% of configurations
- At $20/review and above: HITL never beats baseline

In a realistic AML environment where analyst review costs $20 or more per case, automation dominates across every tested parameter combination. Full results and the regime heatmap are in SENSITIVITY_ANALYSIS.md and figures/hitl_regime_heatmap.png.

---

## Summary of Findings

1. Cost-sensitive thresholding alone is often more impactful than adding human review.
2. Naive HITL policies worsen system performance despite improving local accuracy.
3. Selective HITL is viable only under narrow economic conditions — low review cost, high FN cost, tight allocation.
4. HITL effectiveness is regime-dependent. It is not a property of the model or the reviewers — it is a property of the cost structure.
5. Get the threshold right before adding humans. In most configurations we tested, threshold optimization alone captured the majority of available cost savings — no review required.
