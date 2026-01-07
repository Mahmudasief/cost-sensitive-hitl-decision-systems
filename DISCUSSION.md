# Discussion

This work reframes human-in-the-loop (HITL) decision systems as economic decision problems rather than accuracy optimization tasks. The results demonstrate that the effectiveness of human review is not universal, but highly conditional on cost asymmetry, review cost, and review allocation strategy. In this section, we interpret the empirical findings, discuss their implications for deployment and research, and outline key limitations.

## Why HITL Often Fails in Practice

A central finding of this study is that naïvely applied HITL policies can increase total expected cost even when human reviewers outperform automated models on specific error types, such as false positives. This failure arises from a mismatch between local performance improvements and global system objectives.

In particular, improvements in accuracy on reviewed cases do not necessarily translate into reductions in total expected cost when review costs are non-trivial or when review effort is allocated to low-impact cases. These results help explain why many real-world HITL systems experience persistent investigator overload despite ongoing investments in manual review.

Our findings suggest that the common assumption—human review is always beneficial—is an artifact of evaluating HITL systems using accuracy-centric metrics rather than cost-sensitive objectives.

## Decision Policy Versus Model Choice

An important implication of our results is that decision policy can dominate model choice under asymmetric error costs. Across all observed empirical regimes, transitions between automation-dominant, selective HITL, and HITL-dominant failure modes occur without retraining the underlying classifier.

This indicates that threshold selection and review allocation are first-order determinants of system-level performance in high-stakes decision systems. In many operational environments, optimizing the decision layer yields larger economic gains than improving predictive accuracy through model retraining.

This challenges prevailing research emphasis on model-centric improvements and highlights the need to study HITL systems as integrated socio-technical decision pipelines.

## Implications for Deployment

The results suggest that HITL systems should not be deployed by default. Instead, human review should be treated as an economic intervention whose value depends on explicit cost modeling.

In practice, this implies that:
- Automated decision thresholds should be optimized for cost before introducing human review.
- Review capacity should be selectively allocated to cases near the decision boundary or with the highest marginal expected cost reduction.
- Fixed-rate or indiscriminate review policies are likely to degrade system performance in many realistic cost regimes.

Absent explicit cost modeling, HITL systems may increase operational burden rather than reduce risk, even when human reviewers are highly accurate.

## Limitations

This study makes several simplifying assumptions that delimit the scope of the conclusions.

First, human review accuracy and cost are modeled as fixed and exogenous. In practice, reviewer performance may vary across investigators, over time, and with workload. While sensitivity analyses indicate that the qualitative regime structure is robust across wide parameter ranges, modeling dynamic human behavior remains an important direction for future work.

Second, the analysis assumes a fixed underlying classifier and does not incorporate retraining, feedback loops, or active learning. This is a deliberate design choice to isolate decision-layer effects. Incorporating retraining could shift regime boundaries but would not eliminate the fundamental trade-offs identified here.

Third, the empirical evaluation relies on AML-style datasets and synthetic cost parameters rather than proprietary bank data. The contribution of this work is methodological rather than benchmark-driven: the results concern decision-policy structure and cost trade-offs, which are dataset-agnostic under standard supervised learning assumptions.

Finally, the decision policies considered are static. Extensions to dynamic or sequential decision-making frameworks, such as bandit-based review allocation, are left for future research.

## Summary

Overall, this work demonstrates that HITL effectiveness is not a property of human accuracy alone, but of how and where human intervention is deployed within a cost-sensitive decision system. By explicitly modeling economic trade-offs at the decision layer, the results provide a principled foundation for understanding when human-in-the-loop systems help—and when they hurt.

