# Discussion

This work reframes human-in-the-loop (HITL) decision systems as economic decision problems rather than accuracy optimization tasks. Our results demonstrate that the effectiveness of human review is not universal, but highly conditional on cost asymmetry, review cost, and review allocation strategy. In this section, we interpret the empirical findings, discuss implications for deployment and research, and clarify the limits of the analysis.

## Why HITL Often Fails in Practice

A central finding of this study is that naïvely applied HITL policies can increase total expected cost, even when human reviewers outperform automated models on specific error types such as false positives. This failure arises from a systematic mismatch between local performance improvements and global system objectives.

Specifically, improvements on reviewed cases do not translate into system-level cost reductions when review costs are non-trivial or when review capacity is allocated to low-impact cases. In such regimes, the marginal benefit of error correction is outweighed by the operational cost of review itself. This mechanism provides a concrete explanation for why many production HITL systems experience persistent investigator overload despite continued investment in manual review.

These findings challenge the widespread assumption that human review is inherently beneficial. That assumption emerges from evaluating HITL systems using accuracy-centric metrics, which fail to capture downstream operational costs and decision-level trade-offs.

## Decision Policy Versus Model Choice

An important implication of our results is that decision policy can dominate model choice under asymmetric error costs. Across all observed empirical regimes, transitions between automation-dominant, selective HITL, and HITL-dominant failure modes occur without retraining the underlying classifier.

This demonstrates that threshold selection and review allocation are first-order determinants of system-level performance in high-stakes decision systems. In many operational environments, optimizing the decision layer yields larger economic gains than improving predictive accuracy through model retraining.

This result challenges the prevailing model-centric emphasis in HITL research and highlights the need to study human review as part of an integrated decision pipeline rather than as a post-hoc accuracy enhancement.

## Implications for Deployment

The results suggest that HITL systems should not be deployed by default. Instead, human review should be treated as an economic intervention whose value must be justified under explicit cost assumptions.

In practice, this implies that:

  - Automated decision thresholds should be optimized for total expected cost before introducing human review.

  - Review capacity should be selectively allocated to cases with the highest marginal expected cost reduction.

  - Fixed-rate or indiscriminate review policies are likely to degrade system performance across many realistic cost regimes.

Absent explicit cost modeling, HITL systems may increase operational burden rather than reduce risk—even when human reviewers exhibit high local accuracy.

## Limitations

This study adopts several simplifying assumptions that delimit the scope of the conclusions.

First, human review accuracy and cost are modeled as fixed and exogenous. In real-world settings, reviewer performance varies across individuals, over time, and with workload. While sensitivity analyses indicate that the qualitative regime structure is stable across wide parameter ranges, modeling endogenous and dynamic human behavior remains an important direction for future work.

Second, the analysis assumes a fixed underlying classifier and does not incorporate retraining, feedback loops, or active learning. This is a deliberate design choice to isolate decision-layer effects. Incorporating retraining may shift regime boundaries but would not eliminate the fundamental cost trade-offs identified here.

Third, the empirical evaluation relies on AML-style datasets and abstracted cost parameters rather than proprietary bank data. The contribution of this work is methodological rather than benchmark-driven: the findings concern decision-policy structure and cost asymmetry, which are dataset-agnostic under standard supervised learning assumptions.

Finally, the decision policies considered are static. Extensions to dynamic or sequential decision-making frameworks—such as bandit-based or adaptive review allocation—are left for future research.

## Summary

Overall, this work demonstrates that HITL effectiveness is not a function of human accuracy alone, but of how human intervention is embedded within a cost-sensitive decision system. By explicitly modeling economic trade-offs at the decision layer, we show when human-in-the-loop systems reduce operational cost—and when they systematically increase it.

