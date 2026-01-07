## Title (working)
When Human Review Increases Expected Cost: Cost-Sensitive Analysis of Human-in-the-Loop Decision Systems

## Abstract

Human-in-the-loop (HITL) decision systems are widely deployed in high-stakes domains such as anti-money laundering (AML) under the assumption that human review reduces system risk. However, when decisions incur asymmetric error costs and non-trivial review expenses, human intervention can increase total expected operational cost rather than reduce it. This study examines HITL decision systems through a cost-sensitive lens, asking when human review improves economic outcomes—and when it systematically increases total expected cost.

Using a supervised fraud detection setting with severe class imbalance, we evaluate decision-layer policies—including cost-sensitive thresholding and multiple HITL strategies—using total expected cost rather than predictive accuracy. We show that optimizing the decision threshold alone can substantially reduce system-level false positives and total cost without retraining the underlying classifier. However, HITL interventions do not universally improve outcomes. Across many cost regimes, naively applied human review policies increase total expected cost despite reducing false positives.

Economic gains from HITL arise only under constrained conditions: false-negative costs must be sufficiently high, human review costs sufficiently low, and manual review selectively allocated to the highest-risk cases. In low false-negative or high human-cost regimes, HITL strictly degrades system-level performance. These results demonstrate that the effectiveness of HITL in AML systems is cost-regime dependent and cannot be justified without explicit economic modeling.

This work provides a counterexample to the prevailing assumption that human intervention is inherently beneficial and reframes HITL as a decision-layer optimization problem rather than an accuracy enhancement. Our findings offer principled guidance for deploying manual review only when cost asymmetry, workload constraints, and error trade-offs jointly justify intervention.
