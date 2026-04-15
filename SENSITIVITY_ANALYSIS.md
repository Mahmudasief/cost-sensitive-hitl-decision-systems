# Sensitivity Analysis

## Does the Main Finding Hold Across Cost Assumptions?

The primary analysis uses a specific cost configuration: false-positive cost = $5, false-negative cost = $500, human review cost = $20 per case. These are reasonable AML-style parameters, but any reviewer will ask whether the finding — that HITL does not beat the automated baseline — is specific to this configuration or holds more broadly.

We tested 240 combinations of cost parameters to find out.

## What We Varied

| Parameter | Values |
|---|---|
| False-positive cost | $1, $5, $10, $20 |
| False-negative cost | $50, $100, $200, $500, $1,000 |
| Human review cost | $5, $10, $20, $50 |
| Review rate | 5%, 10%, 20% |

This gives 4 x 5 x 4 x 3 = 240 configurations. For each one, we asked: does any HITL policy beat the automated RF baseline at threshold 0.05?

## What We Found

45 out of 240 configurations (18.75%) show HITL beating the baseline. The other 202 configurations (81.25%) show HITL increasing total expected cost.

The pattern is summarized in the regime heatmap (figures/hitl_regime_heatmap.png). What stands out is not which configurations HITL wins — it is what determines whether HITL wins at all.

**False-negative cost has essentially no effect on the outcome.** Whether a missed fraud case costs $50 or $1,000, the regime pattern is identical across all five FN cost levels:

| Human Review Cost | Win Rate Across All FN Costs |
|---|---|
| $5/case | 50% |
| $10/case | 25% |
| $20/case | 0% |
| $50/case | 0% |

The only thing that changes whether HITL is viable is how much each review costs. At $20 per case — a conservative floor for analyst time in a compliance setting — automation beats HITL in every single configuration we tested, regardless of how severe the false-negative cost is.

This sharpens the main finding considerably. The question is not whether false negatives are expensive enough to justify human review. The question is whether review itself is cheap enough — and in most realistic AML environments, it is not.

## A Note on Statistical Testing

These results are deterministic. The classifier is fixed, the test set is fixed, and the cost calculations are arithmetic on exact counts. There is no randomness in the pipeline — running the same configuration twice gives the same number. Statistical significance testing assumes a sampling distribution, which requires stochastic variation. That does not exist here.

Sensitivity analysis across parameter ranges is the right way to demonstrate robustness for a deterministic system, and that is what the table above provides.
