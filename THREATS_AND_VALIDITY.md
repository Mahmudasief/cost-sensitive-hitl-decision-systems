# Threats to Validity and Reviewer Objections

## Threats to Internal Validity

### Simplified Human Review Model

Human reviewers are modeled using fixed accuracy and cost parameters. In real AML operations, reviewer accuracy varies across investigators, changes over time, and degrades with workload. None of that is captured here.

**Mitigation:** The goal is not to model human cognition — it is to analyze decision-layer economics. We ran sensitivity analyses across reviewer correction probabilities from 0.5 to 0.9 and the regime structure held throughout. The qualitative finding does not depend on any specific assumption about how accurate human reviewers are.

### Fixed Cost Parameters

False-positive, false-negative, and review costs are treated as fixed throughout the analysis.

**Mitigation:** These are abstracted operational costs, not literal dollar figures. The analysis is explicitly regime-based — conclusions are stated conditionally, not as universal cost estimates. The sensitivity analysis in SENSITIVITY_ANALYSIS.md shows that the qualitative pattern holds across wide ranges of all three cost parameters.

---

## Threats to External Validity

### Domain Specificity

The empirical evaluation uses AML-style fraud detection as its setting. Fraud detection has specific characteristics — severe class imbalance, asymmetric error costs, high-volume transaction data — that may not generalize to every HITL deployment.

**Mitigation:** The cost-sensitive decision framework applies to any binary classification system with asymmetric error costs and optional human review. AML is the motivating application, but the findings about cost regimes and decision-layer optimization are not domain-specific. The same analysis applies to medical triage, content moderation, or any setting where review has a meaningful cost.

### Use of Public Dataset

The study uses the Kaggle credit card fraud dataset rather than proprietary bank data.

**Mitigation:** The contribution is methodological, not a benchmark. The paper makes claims about cost-regime structure and decision-policy effects, not about absolute fraud detection performance. Those claims hold regardless of which dataset is used, provided the cost model is correctly specified.

---

## Modeling Assumptions and Scope

### No Model Retraining

The classifier is held fixed throughout. There is no retraining, no active learning, no feedback from human corrections back into the model.

**Rationale:** This is deliberate. Retraining would confound the decision-layer effects we are trying to isolate. The question is what threshold selection and review allocation can accomplish given a fixed model — not what a better model might achieve.

### Static Review Policies

HITL policies are evaluated as fixed rules, not as adaptive or sequential decision processes. The system does not learn from past review decisions or adjust allocation over time.

**Rationale:** Most production AML systems operate this way. Static rule-based review allocation is the norm, not the exception. Extensions to dynamic or bandit-based policies are a natural direction for future work.

---

## Anticipated Reviewer Objections

### Objection 1: "Humans outperform models on reviewed cases, so HITL must help"

**Response:** Local accuracy on reviewed cases and global system cost are different things. We show repeatedly that human reviewers can outperform the model on false positives within the reviewed subset while the total system cost still goes up. The mechanism is simple: review costs money, and those costs can exceed the value of the corrections made.

### Objection 2: "These cost settings are unrealistic"

**Response:** The primary cost configuration (FP=$5, FN=$500, review=$20) is a stylized AML setting, not a claim about real bank numbers. The sensitivity analysis tests 240 combinations across wide parameter ranges. The finding — that HITL is unviable when review costs $20 or more per case — holds across all of them.

### Objection 3: "Practitioners already know this"

**Response:** If practitioners know it, production systems do not show it. HITL is routinely deployed without explicit cost modeling, and investigator overload is a persistent complaint in AML operations precisely because review volume is not calibrated against expected cost savings. Knowing something intuitively and operationalizing it formally are different things.

### Objection 4: "The contribution is incremental"

**Response:** Prior HITL work evaluates systems on classification metrics — precision, recall, AUC. This paper evaluates on total expected cost and shows that accuracy improvements and cost reductions are not the same thing, and can move in opposite directions. That reframing, plus the formal negative result and the failure taxonomy, is not an incremental contribution to the existing literature.

### Objection 5: "No statistical significance testing is reported"

**Response:** This objection misapplies the concept. Statistical significance testing is for stochastic processes — situations where results vary across repeated trials due to randomness. This pipeline has no randomness. The classifier is fixed, the test set is fixed, cost calculations are arithmetic on exact counts. Running the same configuration twice gives the same number. P-values are not meaningful here and reporting them would misrepresent the nature of the analysis.

Robustness for a deterministic system is demonstrated by showing the finding holds across a range of parameter assumptions. That is what SENSITIVITY_ANALYSIS.md does — 240 configurations, wide parameter ranges, stable qualitative result throughout.

---

## Positioning Relative to Prior Work

This paper is not an argument against human review. The claim is narrower: HITL effectiveness depends on cost structure, and deploying review without modeling that structure is likely to increase total operational cost in realistic AML environments.

Prior HITL work has documented when and how human review improves accuracy. That work is not wrong — it answers a different question. This paper asks when human review reduces total operational cost, and finds that the answer depends almost entirely on how expensive that review is, not on how severe the errors are.

The practical implication is not "remove humans from the loop." It is "model the cost before you add humans to the loop."
