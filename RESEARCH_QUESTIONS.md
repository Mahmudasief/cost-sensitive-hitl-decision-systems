## Research Questions
This study investigates whether human-in-the-loop (HITL) interventions can reduce the total expected operational cost of AML transaction monitoring systems, rather than merely improving conventional classification metrics.

## RQ1:
**Question:**  
To what extent can a cost-sensitive machine learning model reduce false positives in AML monitoring without increasing total expected operational cost?
**Motivation:**  
Most AML systems optimize for recall or AUC, ignoring downstream investigation costs. This question evaluates whether cost-aware thresholding alone can meaningfully reduce false positives while remaining economically viable.

##RQ2:
**Question:**  
Under what cost regimes (false-positive cost, false-negative cost, and human review cost) does human-in-the-loop intervention reduce total expected cost compared to a fully automated model?
**Motivation:**  
Human-in-the-loop (HITL) interventions are often assumed to be beneficial by default. This question explicitly tests whether HITL effectiveness is conditional on the economic environment rather than universally advantageous.

##RQ3:
**Question:**  
Does selective human review of high-risk alerts outperform naive HITL policies that apply fixed review rates across all flagged transactions?
**Motivation:**  
This question examines whether *where* human effort is applied matters more than *how much* human effort is applied

##RQ4:
**Question:**  
Can false-positive reduction achieved through HITL be outweighed by increased investigation costs, resulting in higher overall system loss?
**Motivation:**  
This question addresses HITL failure modes, identifying scenarios where human intervention improves apparent model performance while degrading real-world operational efficiency.

##Scope and Assumptions:
The analysis assumes a supervised AML detection setting with class imbalance.
Cost parameters reflect investigation and compliance burden rather than regulatory fines.
Results are evaluated using total expected cost as the primary objective function.
