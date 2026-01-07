# Results and Empirical Regimes

## Overview

We evaluate automated and human-in-the-loop (HITL) decision policies across a wide range of cost regimes to understand when human intervention reduces total expected operational cost—and when it does not.

All results are reported in terms of **total expected cost**, not classification accuracy or AUC. The underlying classifier is held fixed throughout.

---

## Baseline: Automated Decision-Making

Across all cost regimes, we first identify the optimal automated threshold that minimizes expected cost without any human review.

This automated baseline serves as the reference point against which all HITL policies are compared.

In several regimes, especially those with moderate false-negative costs and non-trivial review cost, the automated baseline achieves the lowest expected cost among all evaluated policies.

Importantly, none of the top-ranked (lowest total cost) human-in-the-loop (HITL) configurations outperform the automated baseline. All HITL policies that beat the baseline occur outside the extreme low-cost region and require specific cost asymmetries.


---

## Effect of Cost-Sensitive Thresholding

Optimizing the decision threshold alone yields substantial reductions in false positives and total cost relative to standard accuracy-optimized thresholds.

In many regimes, threshold optimization without human review captures the majority of achievable cost savings, highlighting the importance of decision-layer optimization independent of HITL.

---

## Naïve HITL Can Increase Total Cost

We observe that naïvely applied HITL policies—such as fixed-rate review of flagged transactions—can **increase total expected cost**, even when human reviewers outperform the model on false positives.

This cost increase arises from:
- Review costs overwhelming marginal error reduction
- Human effort being allocated to low-impact cases
- Improved local accuracy failing to translate into global cost reduction

These findings contradict the common assumption that adding human review is inherently beneficial.

---

## Selective HITL and Marginal Gains

Selective review strategies that prioritize high-risk or boundary cases can outperform fixed-rate HITL policies in specific cost regimes; however, these strategies still do not achieve lower total expected cost than the optimal automated baseline.


However, the gains from selective HITL are typically **marginal** and occur only when:
- False-negative costs are sufficiently high
- Review costs are sufficiently low
- Review capacity is carefully constrained

Outside these conditions, selective HITL offers little or no advantage over automation.

---

## Empirical Cost Regimes

Our results reveal three distinct empirical regimes:

### Regime I: Automation-Dominant

- Review costs are high relative to error costs
- Optimal policy: **Fully automated decision-making**
- HITL strictly degrades system-level performance

### Regime II: Selective HITL Advantage

- False-negative costs are high
- Review costs are low
- Review is applied selectively to highest-risk cases
- HITL yields modest reductions in expected cost
- Improvements occur away from the global cost minimum and do not dominate the optimal automated policy


### Regime III: HITL-Dominant Failure

- Review is applied broadly or indiscriminately
- Local accuracy improves on reviewed cases
- Total expected cost increases due to operational overhead

These regimes are stable across wide ranges of reviewer accuracy and model calibration.

---

## Decision Policy Dominates Model Choice

Crucially, all observed regime transitions occur **without retraining the model**.

This demonstrates that, under asymmetric error costs, decision policy and review allocation can dominate model choice as determinants of system-level performance.

---

## Summary of Findings

1. Cost-sensitive thresholding is often more impactful than adding human review.
2. Naïve HITL policies can worsen system performance despite improving local accuracy.
3. Selective HITL is beneficial only under narrow and explicit economic conditions.
4. HITL effectiveness is regime-dependent, not universal.
5. Decision-layer optimization is a first-order concern in high-stakes ML systems.



