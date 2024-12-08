# Credit Card Fraud Detection Model

This is the final project of IS 451 (Business Analytics) conducted by Tom Kasimov, Joshua Chen, Ismael Ponce, Alex Edwards, Ben Glassmire. The project aimed to compare the performance of different statistical models in credit card fraud classifications. 
![credit-card-fraud](credit-card-fraud.jpg)

## Data Setting
**[Credit Card Transactions](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud#)**: This dataset is collected from Kaggle. According to the description of this dataset, it contains transactions made by credit cards in September 2013 by European cardholders. This dataset presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions. The dataset is highly unbalanced, the positive class (frauds) account for 0.172% of all transactions. Given the imbalanced dataset, we would use Recall, F1, Average Precision(AP), and AUC-ROC instead of confusion matrix accuracy to evaluate the performance. The variables in the dataset were processed through PCA transformation, and due to confidentiality issues, we don't know the original features and more background information about the data. The only features which have not been transformed with PCA are 'Time' and 'Amount'.

## Challenges
1. **Accuracy as a Misleading Metric:** A naive model predicting all transactions as non-fraud would achieve ~99.8% accuracy but fail to detect any fraud.
2. **Emphasis on Recall:** In fraud detection, missing a fraudulent transaction (false negative) is typically more costly than flagging a legitimate one (false positive). Thus, recall is critical.
3. **Precision-Recall Trade-off:** While recall captures more fraud cases, precision must be high enough to avoid overwhelming investigators with false positives.

## Modeling Results
### Logistic Regression Model #1
Confusion Matrix
|               |   0(Predict)  |   1(Predict)  |
| ------------- | ------------- | ------------- |
|    0(Actual)  |     85295     |      12       |
|    1(Actual)  |      51       |      85       |

Recall: 0.625  
Precision: 0.8763  
F1 Score: 0.7296  
AP: 0.5483  
AUC: 0.9803  
![ROC Curve Logit 1](https://github.com/user-attachments/assets/6d100f80-f983-40e5-9f21-8a7876a5a1dc)  

#### Model Analysis
•	The model achieves excellent AUC scores (>0.98), indicating a strong ability to rank transactions by fraud likelihood.  
•	Recall (62.5%) is moderate, leaving many fraud cases undetected. Improving recall through techniques like threshold adjustment or oversampling minority classes might help.  
•	Precision is high (~87%), which is desirable to limit false alarms. This is important for resource efficiency when investigating flagged transactions.  
•	AP (0.5483) indicates moderate performance, with precision declining significantly as recall increases.
•	Recommendation: Suitable if a balance between minimizing false positives and capturing fraud is desired.  

### Logistic Regression Model #2
Confusion Matrix
|               |   0(Predict)  |   1(Predict)  |
| ------------- | ------------- | ------------- |
|    0(Actual)  |     85293     |      14       |
|    1(Actual)  |      49       |      87       |

Recall: 0.6397  
Precision: 0.8614  
F1 Score: 0.7342  
AP: 0.5516  
AUC: 0.9812  
![ROC Curve Logit 2](https://github.com/user-attachments/assets/d54fbb0d-5595-4c38-932a-1c6cfe28a4be)

#### Model Analysis
•	Slightly improvement on AUC scores compared to model #1.  
•	Recall improved slightly (63.97%) compared to Model #1, capturing more fraud cases.  
•	Precision decreased slightly (86.14%), indicating slightly more false positives.  
•	A slight improvement over Model #1 on AP (0.5516), indicating a better trade-off between precision and recall across all levels. This suggests Model #2 is marginally better at maintaining precision as recall increases.  
•	Recommendation: Suitable if a balance between minimizing false positives and capturing fraud is desired.  

### CART Model 
Confusion Matrix
|               |   0(Predict)  |   1(Predict)  |
| ------------- | ------------- | ------------- |
|    0(Actual)  |     85292     |      15       |
|    1(Actual)  |      26       |      110      |

Recall: 0.8088  
Precision: 0.8800  
F1 Score: 0.8429  
AP: 0.7121  
AUC: 0.9409  
![ROC Curve CART](https://github.com/user-attachments/assets/08ca5ba3-4a9a-4f32-8d1e-58c1b81f765d)  

#### Model Analysis
•	The CART model excels in recall (80.88%), detecting most fraud cases, making it highly effective for high-stakes scenarios where missing fraud is unacceptable.  
•	Precision (88%) is also high, meaning it doesn’t produce an overwhelming number of false positives despite the higher recall.  
•	The highest AP score among all models, reflecting its superior ability to sustain high precision even at higher recall levels.  
•	AUC (0.9409) is slightly lower than the logistic models, but the trade-off for improved recall is often worthwhile in fraud detection.  
  
•	Recommendation: Best suited for scenarios prioritizing recall.  

### Random Forest Model
Confusion Matrix
|               |   0(Predict)  |   1(Predict)  |
| ------------- | ------------- | ------------- |
|    0(Actual)  |     85288     |      19       |
|    1(Actual)  |      48       |      88       |

Recall: 0.6518  
Precision: 0.8224  
F1 Score: 0.7273  
AP: 0.5327  
AUC: 0.9822  
![ROC Curve RF](https://github.com/user-attachments/assets/956610a0-c423-4f4a-814e-44eb317aedda)  

#### Model Analysis
•	This model offers the highest AUC (0.9822), indicating excellent discrimination capability.  
•	However, recall (65.18%) and precision (82.24%) are lower compared to the CART model, suggesting suboptimal handling of the imbalanced data.  
•	The lowest AP score, indicating that while Random Forest achieves high precision initially, it struggles to maintain it as recall increases.  
•	Recommendation: Suitable if the primary goal is ranking transactions by fraud likelihood but not necessarily maximizing recall.  

## Key Findings
The evaluation of the models highlights important trade-offs between precision and recall. Logistic regression models prioritized precision, reducing false positives but missing some fraudulent transactions, while the CART model focused on maximizing recall, capturing more fraud cases at the expense of slightly increased false positives. The excellent AUC values achieved by logistic regression and Random Forest make them reliable for ranking transactions by fraud likelihood. Among the models, Logistic Regression Model #2 strikes the best balance of precision and recall, making it the most versatile and reliable choice for this dataset. The CART model, however, is better suited for applications where identifying as many fraud cases as possible is critical, particularly in systems where missing fraud cases could have severe financial or operational consequences. Random Forest and Logistic Regression Model #1 performed well but may not be optimal depending on specific business requirements. Overall, selecting the most appropriate model depends on the priorities of the fraud detection system, such as minimizing false positives, maximizing fraud detection, or achieving a balance between the two.  

## Implications and Limitations
The project highlights several implications for credit card fraud detection. First, the use of PCA transformation reduces the interpretability of the models, making it difficult to understand the original features driving fraud predictions. This lack of insight into specific transactional patterns can limit actionable strategies for fraud prevention. Second, the imbalanced nature of the dataset significantly impacts model evaluation. Metrics like recall, F1 score, AUC-ROC, and AP are crucial for performance assessment, as traditional accuracy metrics can be misleading. Finally, model selection depends on the specific business context. For example, the CART model’s high recall is ideal for scenarios where missing fraudulent transactions carries significant costs, while logistic regression models offer a balanced and interpretable approach suitable for broader applications.  

However, the study also faces limitations. The dataset’s context—transactions from only two days involving European cardholders—restricts the generalizability of the results to other geographies, time periods, or behavioral patterns. Finally, selecting an appropriate decision threshold remains a challenge, as it involves critical trade-offs between minimizing false negatives and controlling false positives, depending on the specific use case.
