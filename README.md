# syriatel-churn-analysis


## Overview
Our client, SyriaTel, is a telecommunication company and is suffering from a loss of valuable customers to competitors.

Understanding customer churn is essential to evaluating the effectiveness of the company’s marketing efforts and the overall satisfaction of the customers. It’s also easier and less expensive to keep existing customers versus to acquire new ones.

Therefore, we are hired to help the management team understand what features are primary determinants of the customer churn. We will further build a classification model to predict whether a customer will (“soon”) stop doing business with SyriaTel.
## Objectives
- Conduct an exploratory data analysis on the existing dataset, which has been obtained from Kaggle.
- Establish a  baseline model using logistic regression.
- Apply machine learning algorithm Decision Tree to build a classifier
- Use the model for classification

## Summary 
### Exploratory Data Analysis
1. Current Churn Rate = 14.5%
2. Churn vs International Plan and Voice Mail Plan

![churn1](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/churn%201.png)![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/churn%20vs%20voice%20mail.png)


3.Churn vs Customer Service Calls
![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/churn%20vs%20customer%20service%20calls.png)

4. Churn vs Average Monthly Charge
![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/churn%20vs%20average%20monthly%20charge.png)



### Baseline model

We built our baseline model following the below process: 

#### (1) Setting up Data and Train/Test Split:
- We identified the target variable and features, including categorical variables like 'state'.
- Categorical variables were encoded using one-hot encoding to represent them numerically.
- The dataset was split into training and testing sets to assess model performance.
#### (2) Logistic Regression Model with Cross-Validation:
- We instantiated a Logistic Regression model with random_state=42 to ensure reproducibility of results.
- Cross-validation was performed using cross_val_score with scoring='neg_log_loss' to evaluate the model's performance on the training data.
#### (3) Preprocessing with StandardScaler and SMOTE:
- To enhance model performance and address potential issues like class imbalance, we applied preprocessing techniques.
- StandardScaler was used to standardize features, ensuring mean of 0 and standard deviation of 1.
- Synthetic Minority Over-sampling Technique (SMOTE) was employed to handle class imbalance, generating synthetic samples for the minority class.
#### (4) Reducing Regularization:
- We reduced the regularization effect by instantiating a new Logistic Regression model with lower regularization.
- By adjusting the regularization parameter (C) to a lower value, we allowed the model to fit the training data more closely, potentially improving performance on unseen data.
#### (5) Adjusting gradient descent parameters

Upon the preprocessing procedures, we got our baseline model. The validation results are:
![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/logistic%20regression.png)

##### AUC: 0.8187870239774331

![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/confusion%20matrix%20baseline%20model%20.png)

### Building A classification model

Given the class imbalance (84% non-churn, 16% churn), our primary focus is on evaluating the model's performance concerning the churn cases (the minority class).

- The F1 Score, which is the harmonic mean of Precision and Recall, provides a balanced assessment of the model's performance on the churn class. It considers both the precision (the proportion of correctly predicted churn cases among all predicted churn cases) and recall (the proportion of correctly predicted churn cases among all actual churn cases).

- The Recall Score specifically emphasizes the model's ability to identify customers who churned but were not correctly predicted by the model. It measures the proportion of actual churn cases that the model successfully predicted.

- Additionally, we consider the AUC (Area Under the Receiver Operating Characteristic curve) score. A perfect classifier would have an AUC score of 1.0, indicating perfect discrimination between positive and negative cases. On the other hand, an AUC of 0.5 is considered trivial or worthless, implying no discrimination ability beyond random chance.

![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/roc%20dtc.png)

##### AUC: 0.9212016925246826

![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/confusion%20matrix%20decision%20tree%20classifier.png)

### Feature Importance 

![](https://github.com/musairshad/syriatel-churn-analysis/blob/main/images/feature%20importance.png)

The primary determinants of the customer churn are customer service calls, monthly charge, international plan and number of vmail messages.

### Conclusion

- The F1 Score is 94%, which means it's really good because F1 Scores can be between 0 and 1. A score of 1 means the model is perfect at putting each observation into the right group, and 0 means it can't do it right at all. So, our model is very good at predicting if customers will stay with or leave SyriaTel. This helps SyriaTel act quickly to keep customers who might be thinking of leaving.
- The Accuracy Score is 94%, meaning our model is right about whether customers will stay or leave around 94% of the time.
- The Precision Score is 75%, which means when our model predicts a customer is going to leave, it's correct about 75% of the time.
- The Recall Score is 90%, meaning if a customer is actually going to leave, our model will correctly identify them as such about 90% of the time. There's a small 10% chance it might mistakenly think they're going to stay.

We know that gaining new customers is more expensive than keeping current ones. So, if we wrongly predict that a customer who's actually going to leave will stay, it could cost SyriaTel more. That's why we focused on maximizing the 'recall score'.
### Determinants of whether a customer will churn or not

We utilized the 'feature importance' function to identify the key factors influencing whether a customer will churn. The top 4 features identified are: whether the customer has an international plan, the frequency of voicemail messages, the monthly billing charges, and the number of customer service calls made by the customer.
- International Plan : Having an international plan increases the likelihood of a customer leaving. This is because international call charges are much higher than domestic rates. If competitors offer cheaper international calls, customers with international plans may switch providers.

- Monthly Charges : Customers with higher monthly charges are also more likely to churn, as high bills are a major concern for those considering leaving.

- Customer Service callsFrequent: calls to customer service indicate potential churn, as customers typically reach out with issues or complaints. These points of frustration during customer interactions present significant challenges for retaining customers.
- Number of voicemails: a high number of voicemails can contribute to customer churn by signaling communication issues, unresolved problems, feelings of neglect, and a lack of engagement from the company's side.

In summary, customers who have an international plan, receive more voicemails, incur higher monthly bills, and make frequent calls to customer service are more likely to churn.














