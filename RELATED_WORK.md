# Related Work

This work sits at the intersection of human-in-the-loop (HITL) decision systems, cost-sensitive learning, and high-stakes operational deployment. Prior literature has largely treated these areas in isolation or evaluated HITL effectiveness through accuracy-centric metrics. We review the most relevant strands and clarify how this work departs from existing assumptions.

---

## Human-in-the-Loop Decision Systems

Human-in-the-loop systems are widely studied in machine learning, human–computer interaction, and applied AI, particularly in domains such as content moderation, medical triage, fraud detection, and risk assessment. Prior work generally motivates HITL architectures by arguing that human judgment can correct model errors, improve fairness, or handle ambiguous cases that automated systems struggle with.

Most empirical studies evaluate HITL performance using local classification metrics, such as accuracy on reviewed cases, human–model agreement, or reductions in specific error types (e.g., false positives). In these settings, human review is typically assumed to be beneficial by construction, and negative outcomes of HITL intervention are rarely analyzed.

In contrast, this work does not assume that human intervention is inherently beneficial. We explicitly evaluate HITL policies using total expected operational cost and show that human review can degrade system-level performance under plausible cost regimes, even when humans outperform models on reviewed decisions.

---

## Cost-Sensitive Classification and Decision Theory

Cost-sensitive learning has a long history in machine learning, focusing on asymmetric misclassification costs and decision-theoretic optimization. Prior work has examined threshold adjustment, loss reweighting, and utility-based evaluation to handle imbalanced classes and unequal error costs.

However, most cost-sensitive approaches focus exclusively on automated classifiers and do not model downstream human review processes. When human intervention is considered, it is often treated as a post hoc correction mechanism rather than as a decision variable with its own cost structure and capacity constraints.

This work extends cost-sensitive decision-making by explicitly modeling manual review as part of the decision policy. Rather than retraining models or modifying loss functions, we study how threshold selection and review allocation jointly determine total expected cost, isolating the role of the decision layer from model training.

---

## HITL in AML and Fraud Detection

In anti-money laundering (AML) and fraud detection systems, manual investigation is a core operational component. Prior industry and academic work emphasizes reducing false positives to alleviate investigator workload, often reporting improvements in alert precision or recall.

Despite this operational focus, most AML studies evaluate performance using classification metrics or alert counts, without explicitly modeling the economic trade-offs between false positives, false negatives, and investigation cost. Human review is generally treated as an unavoidable necessity rather than a policy choice.

This work departs from prior AML literature by treating manual review as a controllable intervention whose value depends on cost asymmetry, review cost, and allocation strategy. Our results show that reducing false positives alone is insufficient to justify HITL intervention and that naive review policies can increase total operational burden.

---

## Negative Results and Failure Analyses

Negative results and failure modes of HITL systems are underrepresented in the literature. Existing work tends to highlight cases where human intervention improves outcomes, while scenarios in which HITL harms performance are rarely formalized or empirically demonstrated.

A small body of work in decision theory and operations research suggests that adding decision stages can introduce inefficiencies under certain cost structures, but these insights have not been systematically applied to modern ML-based HITL systems.

This paper contributes to this gap by providing an explicit failure taxonomy for HITL decision systems, identifying conditions under which human intervention worsens system-level outcomes. By formalizing these failure modes, we complement prior work that focuses exclusively on HITL benefits.

---

## Positioning of This Work

Unlike prior studies, this work:
- Evaluates HITL systems using total expected operational cost rather than accuracy-based metrics.
- Treats human review as a decision variable with explicit cost and capacity implications.
- Focuses on decision-layer optimization without retraining the underlying model.
- Provides empirical counterexamples to the assumption that HITL intervention is universally beneficial.

As a result, this work reframes HITL systems as economic decision processes rather than hybrid classifiers, offering a complementary perspective to existing accuracy-centric approaches.
