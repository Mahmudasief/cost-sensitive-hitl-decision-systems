##Introduction

Human-in-the-loop (HITL) decision systems are widely deployed in high-stakes machine learning applications, including anti-money laundering (AML), fraud detection, content moderation, and medical triage. In such settings, automated classifiers are routinely augmented with manual review pipelines under the assumption that human intervention reliably reduces error and operational risk. As a result, HITL architectures are often treated as a default best practice in production systems.

Despite their prevalence, the effectiveness of HITL systems is rarely evaluated through an explicit economic lens. Real-world decision systems operate under asymmetric error costs: false positives incur investigation and compliance burden, false negatives expose institutions to financial and regulatory risk, and human review introduces substantial operational cost. Nevertheless, HITL systems are typically evaluated using accuracy-centric metrics such as precision, recall, or area under the ROC curve (AUC), rather than total expected operational cost.

This disconnect creates a critical gap between how HITL systems are evaluated in the literature and how they are deployed in practice. Improvements in local accuracy—particularly on reviewed cases—do not necessarily translate into global reductions in system-level cost. In fact, allocating human review without regard to cost structure or review selectivity may increase total expected cost, even when human reviewers outperform automated models on specific error types.

In this work, we study human-in-the-loop decision systems from a cost-sensitive, decision-theoretic perspective. We model AML-style transaction monitoring as a probabilistic classification problem with thresholded decisions and optional manual review, and evaluate policies using total expected cost rather than predictive accuracy. Crucially, our analysis isolates the decision layer: we examine how threshold selection and review allocation determine system-level performance without retraining or modifying the underlying classifier. While AML serves as a motivating application, the formulation applies broadly to high-stakes decision systems with asymmetric error costs and optional human review.

Through extensive empirical evaluation across a wide range of cost regimes, we demonstrate that naïvely applied HITL policies can increase total expected cost, even when human reviewers reduce false positives on reviewed instances. We identify three distinct empirical regimes in which (i) fully automated decision-making is optimal, (ii) selective HITL yields marginal economic gains, and (iii) HITL intervention strictly degrades system-level performance. Notably, these regime transitions occur without retraining the model, indicating that decision policy can dominate model choice in certain operational environments.

These results challenge the prevailing assumption that adding human review is inherently beneficial. Instead, we show that HITL effectiveness is conditional on cost asymmetry, review cost, and review allocation strategy. By reframing HITL evaluation as an economic decision problem rather than an accuracy optimization task, this work provides principled guidance for when human intervention should be deployed, how selectively it should be applied, and when it should be avoided entirely.

## Contributions

This paper makes the following contributions:

 - We present a cost-first evaluation framework for HITL decision systems that explicitly models false-positive, false-negative, and human review costs.

 - We show that substantial system-level performance differences can be achieved through decision-layer optimization alone, without retraining the underlying classifier.

 - We provide a formal negative result, demonstrating that naïve HITL policies can increase total expected cost despite improving local accuracy.

 - We characterize distinct cost regimes governing when automation, selective HITL, or no HITL is optimal.

 - We introduce a failure taxonomy for HITL systems that explains when and why human intervention degrades operational efficiency.






