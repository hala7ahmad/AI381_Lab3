# Model Selection

## The question

The objective of this experiment is to compare three machine learning models for customer churn prediction and select the best model based on predictive performance, fairness across contract types, prediction latency, and model size.

## Candidates

| Candidate | Why I tried it | AUC | F1 | F1 per slice (lowest) | p95 latency (ms) | Size (KB) | MLflow run ID |
|---|---|---|---|---|---|---|---|
| Logistic Regression | Simple, fast, interpretable baseline model. | 0.7982 | 0.4948 | 0.2500 | 4.5460 | 3.5479 | 114e2b783d0f447a81c0347120f750f2 |
| Random Forest | Handles complex relationships and reduces overfitting by combining multiple decision trees. | 0.7589 | 0.4536 | 0.2222 | 17.8957 | 3160.0957 | a516a4854c504274a866804f0c825af7 |
| Gradient Boosting | Combines weak learners sequentially to improve prediction performance. | 0.7476 | 0.4167 | 0.2222 | 5.0926 | 141.6445 | b29f2bcbbafb4b4cac17f7027cde0172 |

## The champion

My selected champion is **Logistic Regression**.

It achieved the highest AUC of 0.7982 and the highest F1 score of 0.4948, outperforming both Random Forest and Gradient Boosting.

It also achieved the lowest prediction latency of 4.5460 ms and the smallest model size of 3.5479 KB.

Furthermore, Logistic Regression achieved the highest minimum F1 score across contract types (0.2500), indicating better worst-slice performance than the other candidates.

Therefore, Logistic Regression provides the best overall balance between prediction accuracy, efficiency, model size, and performance across customer groups.

## My promotion rules

- **Latency budget (p95): 25 ms**, because the model should provide fast predictions and remain within an acceptable response time.
- **Minimum gain to replace the champion (F1 points): 0.02**, because a meaningful improvement is needed before replacing the current model.

A new candidate should also satisfy the latency budget and be evaluated for performance across different contract types before promotion.

## What I would check next

I would investigate whether the model performs poorly for customers with specific contract types, particularly the groups with lower F1 scores.

I would also monitor changes in customer behavior and data distribution that could reduce prediction accuracy over time.

Finally, I would evaluate the model on new unseen data before deploying it in a production environment.