## AML Compliance Under Asymmetric Risk: A Cost-Sensitive Human-in-the-Loop Framework for Financial Crime Detection 

## Abstract

Human-in-the-loop (HITL) decision systems are standard practice in high-stakes domains like anti-money laundering. The assumption built into this architecture is that human review reduces risk. This paper asks whether that assumption holds when you account for what review actually costs.

We study AML-style transaction monitoring as a binary classification problem where a fixed trained classifier assigns risk scores, a threshold determines which transactions get flagged, and a review policy determines which flagged cases go to a human analyst. We evaluate everything in terms of total expected cost — false positives, false negatives, and review costs combined — rather than the accuracy metrics that most HITL evaluations rely on.

The short answer is that human review does not reliably reduce total operational cost. Naive review policies — fixed review rates applied regardless of case risk — frequently increase total cost, even when human reviewers are more accurate than the model on the cases they see. The mechanism is simple: when review costs more per case than the expected savings from error correction, the system loses money on every review.

Cost-sensitive threshold optimization, without any human review, often captures the majority of available cost savings on its own. This is the part that surprised us most. Getting the decision threshold right matters more than adding humans to the loop.

Where HITL does help, the conditions are specific. Sensitivity analysis across 240 cost configurations shows that the critical variable is human review cost, not false-negative severity. When review costs $20 or more per case — a conservative floor for analyst time in a compliance setting — automation dominates across every cost configuration we tested, regardless of how severe the false-negative cost is. HITL becomes viable only when review is cheap, false-negative costs are high, and review is concentrated on the highest-risk cases.

This paper reframes HITL not as a default safeguard but as a conditional economic intervention. The question is not whether to add human review — it is whether the expected cost reduction from review justifies its price under your specific cost structure. For most realistic AML configurations, the answer is no.
