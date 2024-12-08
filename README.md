# Credit Card Fraud Detection Model

This is the final project of IS 451 (Business Analytics) conducted by Tom Kasimov, Joshua Chen, Ismael Ponce, Alex Edwards, Ben Glassmire. The project aimed to compare the performance of different statitical models in credit card fraud classifications. 
![credit-card-fraud](credit-card-fraud.jpg)

## Data Setting
**[Credit Card Transactions](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud#)**: This dataset is collected from Kaggle. According to the description of this dataset, it contains transactions made by credit cards in September 2013 by European cardholders. This dataset presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions. The dataset is highly unbalanced, the positive class (frauds) account for 0.172% of all transactions. Given the imbalanced dataset, we would use Recall, F1, Average Precision(AP), and AUC-ROC instead of confusion matrix accuracy to evaluate the performance. The variables in the dataset were processed through PCA transformation, and due to confidentiality issues, we don't know the original features and more background information about the data. The only features which have not been transformed with PCA are 'Time' and 'Amount'.

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

## Implications and Limitations
