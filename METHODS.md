# Methods

## Problem Setting

We study a binary decision problem motivated by anti-money laundering (AML) transaction monitoring, though the formulation applies to any high-stakes classification system with asymmetric error costs and optional human review.

Each instance \( x \) is associated with a latent label \( y \in \{0,1\} \), where \( y=1 \) denotes illicit or high-risk activity. A trained probabilistic classifier produces a risk score \( s(x) \in [0,1] \), interpreted as an estimate of \( \mathbb{P}(y=1 \mid x) \).

The system must assign one of three actions to each instance:
1. **Automatic accept**
2. **Automatic reject / flag**
3. **Manual review**, after which a human reviewer issues a final decision

Our objective is to design decision policies that minimize **total expected operational cost**, rather than optimize predictive accuracy.

---

## Cost Model

We model asymmetric costs associated with system decisions:

- \( C_{FP} \): cost of a false positive (legitimate transaction flagged)
- \( C_{FN} \): cost of a false negative (illicit transaction missed)
- \( C_{R} \): cost of manual human review
- \( \alpha \in [0,1] \): probability that a human reviewer correctly corrects a model error

Costs are treated as exogenous and fixed within each experimental regime. They represent abstract operational burden rather than literal monetary values.

---

## Baseline Automated Decision Rule

The baseline automated system applies a single threshold \( \tau \) to the model score:

\[
\hat{y}(x) =
\begin{cases}
1 & \text{if } s(x) \ge \tau \\
0 & \text{otherwise}
\end{cases}
\]

The expected cost of the automated system depends on the induced false-positive and false-negative rates under threshold \( \tau \).

---

## Human-in-the-Loop (HITL) Policies

We evaluate multiple HITL policies that augment the automated classifier with manual review.

### Fixed-Rate Review

A fixed fraction \( r \in [0,1] \) of flagged transactions is randomly selected for manual review, independent of score magnitude.

### Selective Top-Risk Review

Manual review is applied only to instances whose scores fall within a specified interval \( [\tau, \tau + \delta] \), prioritizing cases near the decision boundary or at highest estimated risk.

---

## Decision Outcomes with Review

For reviewed instances:
- A review cost \( C_R \) is incurred
- With probability \( \alpha \), the human reviewer corrects the model’s decision
- With probability \( 1-\alpha \), the model’s decision remains unchanged

This formulation explicitly separates **human accuracy** from **system-level effectiveness**, allowing local improvements to be evaluated against global cost.

---

## Total Expected Cost

For a given policy \( \pi \), total expected cost is defined as:

\[
\mathbb{E}[C \mid \pi] =
C_{FP} \cdot \mathbb{P}(\text{FP}) +
C_{FN} \cdot \mathbb{P}(\text{FN}) +
C_R \cdot \mathbb{P}(\text{review})
\]

All results are reported in terms of total expected cost, not accuracy, precision, recall, or AUC.

---

## Decision-Layer Optimization

Crucially, we do **not** retrain or modify the underlying classifier.

All performance differences arise from:
- Threshold selection
- Review allocation strategy
- Cost regime variation

This isolates the **decision layer** as the object of study and avoids confounding effects from model capacity or training dynamics.

---

## Evaluation Protocol

We evaluate each policy across a grid of cost regimes defined by varying:
- \( C_{FP} / C_{FN} \) ratios
- Review cost \( C_R \)
- Reviewer accuracy \( \alpha \)

For each regime, we identify the cost-minimizing policy and compare it to both fully automated and naïve HITL baselines.

---

## Scope and Assumptions

Our analysis assumes:
- A fixed trained classifier
- Static, one-shot decisions (no sequential feedback)
- Independent instances
- Reviewer behavior summarized by a single correction probability

These assumptions are deliberate and serve to isolate decision-policy effects rather than model learning dynamics.
