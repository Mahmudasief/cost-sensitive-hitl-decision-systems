# Related Work

This paper sits at the intersection of three bodies of work: human-in-the-loop decision systems, cost-sensitive learning, and applied machine learning for financial crime detection. These areas have developed largely in parallel, and none has directly addressed the question we study here—when does adding human review make a decision system economically worse?

---

## Human-in-the-Loop Decision Systems

HITL systems have attracted sustained attention in machine learning and HCI research, particularly for high-stakes applications like content moderation, medical triage, and fraud detection. The standard motivation is that human judgment catches errors automated systems miss, improving fairness or handling edge cases beyond model competence [Mosqueira-Rey et al., 2023; Monarch, 2021].

The empirical record is more complicated. Bansal et al. [2021] find that AI explanations make humans more likely to accept model recommendations—including wrong ones—and that achieving complementary performance, where a human-AI team outperforms either component alone, proves difficult in practice. Mozannar and Sontag [2020] approach the problem theoretically, framing it as *learning to defer*: given a classifier and a human expert, when should the system route a decision to the human? Their framework assumes a fixed cost structure and optimizes a surrogate loss—an important step, but one that still focuses on prediction error rather than downstream operational cost. 

What is largely missing from this literature is an analysis of when human review makes things worse. Studies tend to report conditions under which HITL helps; failure modes are undercharacterized. This paper fills that gap.

---

## Cost-Sensitive Classification and Decision Theory

The theoretical foundations of cost-sensitive learning are well established. Elkan [2001] shows that under asymmetric misclassification costs, the correct response is to adjust the decision threshold at inference time rather than alter the training procedure. Zadrozny and Elkan [2001] extend this to example-dependent costs, where the penalty for misclassifying a particular instance depends on instance-level features. Fernández et al. [2018] provide a comprehensive treatment of imbalanced classification under cost constraints.

What this literature does not address is the downstream cost of human review itself. Cost-sensitive approaches optimize the classifier's decision boundary; they do not model what happens after a flagged instance enters a human review queue. When review is expensive—as it is in AML, where investigation involves analyst time and compliance overhead—ignoring review cost leads to systematically suboptimal policy design. This paper treats review cost as a first-class component of the optimization problem.

---

## HITL in AML and Fraud Detection

Anti-money laundering is an operationally important application domain for this work. Supervised machine learning for transaction monitoring has been extensively studied, with methods ranging from random forests and gradient boosting to graph neural networks [Chen et al., 2018; Ngai et al., 2011]. Jullum et al. [2020] show that well-calibrated ML models can meaningfully reduce false positive rates compared to rule-based alert systems—an important finding for reducing investigator workload.

What is notable about this literature, however, is how rarely it models investigation cost explicitly. Most AML studies report precision, recall, and AUC; the economic value of a reduced false positive rate is left implicit. And human review—the investigator who receives and closes each alert—is treated as a fixed operational reality rather than as a variable policy choice. Our work reframes this: the decision of how much human review to apply, and to which alerts, is itself a policy that can be optimized or misallocated.

---

## Negative Results and Failure Analyses

Negative results are underrepresented in the HITL literature. The default framing is that human oversight improves AI systems, and most published studies report conditions confirming this. Buçinca et al. [2021] are a notable exception, documenting systematic overreliance—cases where human-AI collaboration performs worse than either party alone—and attributing this to cognitive shortcuts triggered by AI recommendations.

Work in decision theory and operations research has long recognized that adding decision stages can degrade performance under certain cost structures [Raiffa and Schlaifer, 1961], but this insight has not been carried into the applied HITL literature in any systematic way. The closest precedent is the automation bias literature, but that work focuses on human cognition rather than system-level economic outcomes.

This paper takes a different approach: rather than studying how humans respond to AI recommendations, we ask whether human review—regardless of how well it is executed—can be economically justified given the cost structure of the problem. The answer is often no.

---

## How This Work Is Positioned

The contribution here is not that human review is bad. It is that human review is a decision with economic consequences that depend on cost asymmetry, review pricing, and allocation strategy—and that these consequences are rarely modeled explicitly. By treating HITL as a decision policy rather than a default safeguard, this work offers a framework for deciding when human review earns its cost and when it does not.

---

## References

Bansal, G., Wu, T., Zhou, J., Fok, R., Nushi, B., Kamar, E., Ribeiro, M. T., and Weld, D. S. (2021). Does the whole exceed its parts? The effect of AI explanations on complementary team performance. In *Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems*. ACM.

Buçinca, Z., Malaya, M. B., and Gajos, K. Z. (2021). To trust or to think: Cognitive forcing functions can reduce overreliance on AI in AI-assisted decision-making. *Proceedings of the ACM on Human-Computer Interaction*, 5(CSCW1), 1–21.

Chen, Z., Van Khoa, L. D., Nazir, A., Teoh, E. N., and Karupiah, E. K. (2018). Machine learning techniques for anti-money laundering (AML) solutions in suspicious transaction detection: A review. *Knowledge and Information Systems*, 57(2), 245–285.

Elkan, C. (2001). The foundations of cost-sensitive learning. In *Proceedings of the 17th International Joint Conference on Artificial Intelligence (IJCAI)*, pages 973–978.

Fernández, A., García, S., Galar, M., Prati, R. C., Krawczyk, B., and Herrera, F. (2018). *Learning from Imbalanced Data Sets*. Springer.

Jullum, M., Løland, A., Huseby, R. B., Ånonsen, G., and Lorentzen, J. (2020). Detecting money laundering transactions with machine learning. *Journal of Money Laundering Control*, 23(1), 173–186.

Monarch, R. M. (2021). *Human-in-the-Loop Machine Learning*. Manning Publications.

Mosqueira-Rey, E., Hernández-Pereira, E., Alonso-Ríos, D., Bobes-Bascarán, J., and Fernández-Leal, Á. (2023). Human-in-the-loop machine learning: A state of the art. *Artificial Intelligence Review*, 56(4), 3005–3054.

Mozannar, H. and Sontag, D. (2020). Consistent estimators for learning to defer to an expert. In *Proceedings of the 37th International Conference on Machine Learning (ICML)*, PMLR 119:7076–7087.

Ngai, E. W. T., Hu, Y., Wong, Y. H., Chen, Y., and Sun, X. (2011). The application of data mining techniques in financial fraud detection: A classification framework and an academic review of literature. *Decision Support Systems*, 50(3), 559–569.

Raiffa, H. and Schlaifer, R. (1961). *Applied Statistical Decision Theory*. Harvard University Press.

Zadrozny, B. and Elkan, C. (2001). Learning and making decisions when costs and probabilities are both unknown. In *Proceedings of the 7th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, pages 204–213.
