# Discussion

The central result of this paper is simple to state: adding human review to an automated decision system does not reliably reduce total operational cost. Whether it helps or hurts depends on cost structure, and in the most common AML cost configurations we tested, it hurts. This section unpacks what that means and why it matters.

---

## Why Human Review Fails More Often Than Expected

The standard argument for HITL goes like this: humans catch errors models miss, so adding review reduces false positives, and fewer false positives means lower cost. The logic is intuitive but incomplete.

What it misses is that review itself has a cost. Every analyst-hour spent closing an alert is money spent. If the expected benefit of catching an additional false positive — the cost saved by correctly dismissing it — is smaller than the cost of the review that found it, the system is worse off with review than without it. This is not a theoretical edge case. It is what we observe across most of the cost configurations we tested.

The second problem is allocation. Fixed-rate review policies — apply review to some fraction of flagged cases, selected at random or by queue order — waste human effort on cases the model already handled correctly. An analyst reviewing a true positive that would have been correctly flagged anyway contributes nothing to cost reduction. The review cost is incurred; no benefit is realized.

These two mechanisms — review cost exceeding correction value, and effort misallocated to low-impact cases — explain the majority of HITL failure cases we document.

---

## The Decision Layer Is More Powerful Than It Looks

A secondary finding that surprised us: optimizing the decision threshold alone, without any human review, recovered most of the available cost savings.

This matters because it reorders the standard deployment logic. The conventional approach is to train a model, deploy it with a default threshold, and then layer human review on top to handle errors. What our results suggest is that threshold optimization should come first — before any decision about whether to deploy review at all. In many regimes, getting the threshold right makes review unnecessary. In others, it reduces the volume of cases that need review to the point where review becomes cost-effective.

The broader implication is that the decision layer — threshold and review allocation policy — deserves at least as much engineering attention as the model itself. In practice it gets far less.

---

## When HITL Actually Helps

Human review does improve system-level cost under specific conditions, and it is worth being precise about what those conditions are.

The sensitivity analysis across 240 cost configurations makes this unusually clear: the dominant factor is human review cost, not false-negative severity. Whether a missed illicit transaction costs $50 or $1,000, the pattern is the same — HITL only becomes viable when review itself is cheap. Specifically, when review costs $20 or more per case, automation dominates across every cost combination we tested. When review costs $5–$10 per case, selective HITL can yield modest gains.

Review also needs to be allocated selectively — concentrated on the highest-risk flagged cases rather than spread uniformly across the alert queue. Broad review policies waste the cost advantage that cheap review provides.

This conditionality is the core finding. HITL is not a universally good intervention. It is a conditional one, and the primary condition is not how bad your false negatives are — it is how cheap your reviews are.

---

## Limitations

Three limitations of this study are worth being direct about.

First, human reviewer accuracy is modeled as a fixed parameter. Real reviewers vary — across individuals, across time, with workload and fatigue. We ran sensitivity analyses across a range of correction probabilities (0.5 to 0.9) and the qualitative regime structure held, but the exact regime boundaries would shift with more realistic reviewer models.

Second, the classifier is fixed throughout. We deliberately excluded retraining to isolate decision-layer effects, but in practice classifiers are periodically retrained on new data, and retraining shifts the regime boundaries. The decision-policy effects we identify are real, but they interact with model quality in ways this study does not fully capture.

Third, the empirical evaluation uses the public Kaggle credit card fraud dataset as a proxy for AML transaction monitoring. This dataset has known limitations — it is highly imbalanced, features are anonymized via PCA, and it does not reflect the network structure of real money laundering activity. The contribution of this paper is methodological rather than empirical: the cost-regime framework applies regardless of dataset, but the specific numbers reported are not transferable to production AML systems without recalibration.

---

## What This Changes

If the findings hold — and the regime structure is stable enough across parameter ranges that we believe they do — then the standard HITL deployment logic needs to be revised.

The question should not be "should we add human review?" as if review is costless and universally beneficial. The question should be "what is the expected cost reduction from review under our specific cost parameters, and does it exceed the cost of the review itself?" That calculation requires explicit cost modeling. Most production systems do not do it.

This paper does not argue that human review is bad. It argues that human review is expensive, that its benefits are conditional, and that deploying it without cost modeling is a form of optimism that production data does not consistently support.
