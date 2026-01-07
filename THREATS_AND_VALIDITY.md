# Threats to Validity and Reviewer Objections

This section addresses potential threats to validity and anticipates common reviewer objections regarding scope, assumptions, and generalizability of the proposed findings.

## Threats to Internal Validity

### Simplified Human Review Model
Human reviewers are modeled using fixed accuracy and cost parameters. In real AML operations, reviewer accuracy may vary across investigators, over time, and with workload.

**Mitigation:**  
The objective of this study is not to model human cognition but to analyze decision-layer economics. Sensitivity analyses across a wide range of reviewer accuracy and cost parameters demonstrate that the qualitative findings persist across plausible operational regimes.
Specifically, we observe consistent regime boundaries across reviewer correction probabilities ranging from 0.5 to 0.9.

### Assumption of Fixed Cost Parameters
False-positive, false-negative, and review costs are treated as exogenous and fixed.

**Mitigation:**  
These parameters represent abstracted operational burden rather than literal dollar costs. The analysis is explicitly regime-based, and conclusions are framed conditionally on cost asymmetry rather than absolute values.

---

## Threats to External Validity

### Domain Specificity to AML/Fraud Detection
The empirical evaluation focuses on AML-style fraud detection tasks with severe class imbalance.

**Mitigation:**  
The proposed framework applies broadly to any high-stakes decision system with asymmetric error costs and optional human review, including medical triage, content moderation, and risk screening. AML is used as a representative, not exclusive, domain.

### Use of Public or Synthetic Datasets
The study relies on publicly available or AML-style datasets rather than proprietary bank data.

**Mitigation:**  
The contribution is methodological rather than empirical benchmarking; conclusions concern decision-policy structure and cost trade-offs, not absolute performance levels.

---

## Modeling Assumptions and Scope Limitations

### No Model Retraining or Active Learning
The analysis assumes a fixed underlying classifier and does not incorporate retraining, feedback loops, or adaptive learning from human review.

**Rationale:**  
This is a deliberate design choice to isolate decision-layer effects. Incorporating retraining would confound policy-level conclusions and obscure the role of thresholding and review allocation.

### Static Decision Policies
HITL policies are evaluated as static mappings rather than dynamic or sequential decision processes.

**Rationale:**  
The static formulation reflects how most production AML systems are deployed in practice. Extensions to dynamic or bandit-based policies are left for future work.

---

## Anticipated Reviewer Objections

### Objection 1: “Humans outperform models, so HITL should always help”
**Response:**  
Local accuracy improvements do not imply global cost reductions. We show that HITL can increase total expected cost even when human reviewers outperform the model on false positives.

### Objection 2: “Results depend on unrealistic cost settings”
**Response:**  
The paper explicitly avoids universal claims. Results are presented as conditional on cost regimes, and negative outcomes occur across wide, realistic parameter ranges.

### Objection 3: “This is obvious to practitioners”
**Response:**  
Despite practitioner intuition, HITL is routinely deployed without explicit cost modeling. The prevalence of naive review policies in production systems suggests that these trade-offs are not formally operationalized, despite their prevalence in production systems.

### Objection 4: “The contribution is incremental”
**Response:**  
Prior work evaluates HITL primarily through accuracy metrics or human-model agreement. This work reframes HITL as an economic decision problem and provides formal counterexamples to widely held assumptions.

---

## Positioning Relative to Prior Work

This study does not argue against human review per se. Instead, it demonstrates that HITL effectiveness is conditional, not universal. By formalizing failure modes and negative results, the paper complements prior work that focuses exclusively on HITL benefits.

The primary contribution is conceptual: shifting HITL evaluation from accuracy-centric thinking to cost-sensitive decision optimization.

---

## Summary

The key limitation of this work is intentional: abstraction. By simplifying human behavior and focusing on decision-layer economics, we isolate when and why HITL succeeds or fails. This trade-off enables principled insight at the expense of fine-grained behavioral realism.
