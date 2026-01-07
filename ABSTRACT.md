## Title (working)
When Human-in-the-Loop Increases Risk: Cost-Sensitive Analysis of Manual Review Under Asymmetric Error Costs

## Abstract

Anti-money laundering (AML) transaction monitoring systems are commonly evaluated using predictive metrics such as recall or AUC, while largely ignoring downstream operational costs arising from false positives, false negatives, and human investigations. In practice, these costs dominate system performance and determine economic viability. This study examines whether cost-sensitive decision policies and human-in-the-loop (HITL) interventions reduce total expected operational cost, rather than merely improving predictive accuracy.

Using a supervised fraud detection setting with severe class imbalance, we evaluate baseline automated models, cost-sensitive decision threshold optimization, and multiple HITL policies, including fixed-rate and selective top-risk manual review. We show that optimizing the decision threshold alone can substantially reduce system-level false positives and total cost without retraining the underlying classifier. However, HITL interventions do not universally improve outcomes. Across many cost regimes, naively applied human review policies increase total expected cost despite reducing false positives.

Economic gains from HITL arise only under constrained conditions: false-negative costs must be sufficiently high, human review costs sufficiently low, and manual review selectively allocated to the highest-risk cases. In low false-negative or high human-cost regimes, HITL strictly degrades system-level performance. These results demonstrate that the effectiveness of HITL in AML systems is cost-regime dependent and cannot be justified without explicit economic modeling.

This work provides a counterexample to the prevailing assumption that human intervention is inherently beneficial and reframes HITL as a decision-layer optimization problem rather than an accuracy enhancement. Our findings offer principled guidance for deploying manual review only when cost asymmetry, workload constraints, and error trade-offs jointly justify intervention.
