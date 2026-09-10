# Research Positioning Record

## Working research problem

This study examines how limited human review capacity should be allocated after an AI fraud model has already produced calibrated risk probabilities.

The main problem is not only whether a model can identify fraud accurately. In practice, false positives and false negatives have different costs, and organizations cannot send every transaction to a human analyst.

The study therefore asks when human review creates enough value to justify using limited review capacity and which transactions should receive that review.

---

## Positioning of the study

The study treats human review as a constrained post-prediction decision-allocation problem.

The model is trained and calibrated first. Human review is then added as a separate decision layer.

Two transparent review approaches are compared:

1. Two-threshold HITL:
   transactions in an uncertain probability region are sent for review.

2. Cost-targeted HITL:
   transactions are prioritized based on their expected economic value from human review, subject to available review capacity.

The study evaluates how these policies behave under different review capacities, asymmetric error costs, and reviewer-quality assumptions.

The selected policies are then frozen and evaluated on untouched held-out test data. Paired bootstrap analysis is used to quantify uncertainty in the final cost reductions.

---

## What this study does NOT claim

This study does not claim:

- to introduce the first human-in-the-loop fraud system;
- to introduce the first cost-sensitive fraud system;
- to introduce the first capacity-constrained review system;
- to introduce the first learning-to-defer method;
- to introduce reject-option classification;
- to be the first study to consider imperfect human reviewers.

Prior research, including DeCCaF, FiFAR/OpenL2D, selective prediction, reject-option classification, and learning-to-defer research, already addresses parts of these problems.

The novelty must therefore come from the specific decision problem studied and the evidence produced, rather than from claiming that the individual components are new.

---

## Current defensible research gap

Existing research has studied cost-sensitive fraud prediction, selective prediction, reject-option classification, learning to defer, human fallibility, and capacity-constrained allocation.

However, an important deployment problem remains.

An organization may already have a trained and calibrated risk model and limited analyst capacity but may not have enough expert-labeled data to train another human-deferral model.

In this setting, it is still important to determine which transactions should receive scarce human attention, whether uncertainty-based review and economic-value-based review lead to different outcomes, and how the value of human review changes with capacity, reviewer quality, asymmetric costs, and the model's underlying error structure.

This study focuses on that problem.

---

## Current central contribution

The study provides a transparent post-prediction framework for evaluating limited human review in cost-sensitive AI decision systems without requiring a separately trained expert-deferral model.

The empirical analysis shows that the value of human review depends not only on review capacity but also on which cases are reviewed, the economic consequences of different errors, reviewer reliability, and the underlying error composition of the automated system.

The study also distinguishes between the potential value of HITL and the robustness of that value.

A policy may produce a large benefit under favorable reviewer conditions but become fragile when reviewer quality declines. Another policy may provide a much smaller benefit while remaining consistently positive across reviewer-quality scenarios.

---

## Methodological strengths already completed

- Two fraud datasets
- Frozen model-family selection
- Probability calibration
- Cost-sensitive automated threshold selection
- Two transparent HITL allocation policies
- Review-capacity sensitivity analysis
- Cost-ratio sensitivity analysis
- Reviewer sensitivity/specificity analysis
- Joint robustness scenarios
- Frozen-policy evaluation on untouched held-out test data
- Validation-to-test generalization analysis
- Transaction-level reconstruction integrity checks
- 10,000-replicate paired bootstrap uncertainty analysis
- No test-set reoptimization

---

## Important limitations to preserve

Reviewer performance is evaluated using sensitivity/specificity scenarios. These scenarios should not be described as observed behavior of real fraud analysts.

The study does not learn individual analyst performance.

The study does not claim that statistically stable cost reductions are necessarily economically important.

The IEEE-CIS two-threshold result is an important example: the effect remains positive in the bootstrap analysis, but its economic magnitude is negligible.

The study evaluates the framework in fraud detection, so broader decision-support implications must be presented carefully rather than claiming universal generalizability.
