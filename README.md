# project3
project 3 - churn analysis

Data Source:
Our data was sourced from https://github.com/learn-co-students/Mod3-Project_HTX-DS-111819. We had 3 options to choose from, and decided go with 'Customer Churn Data'.

Business problem:
Customers often take advantage of the greatest mobile company deals out there. Is it possible to predict whether a customer will churn or stay with the company? Given  some details such as phone numbers, charges and other features, we are going to build a classifier model to make the predict of whether the company can predict which customers it may lose soon.

Cleaning:
We dropped some columns, including 'phone number', 'area code' and 'state'.
Object columns such as 'international plan' and 'voicemail plan' were encoded to 1s and 0s.
The target column values of True and False were also encoded to 1s and 0s. 1 meaning the customer churned.
For this project, we did not do anything with NaN values.

Metrics:
We started with a baseline model using a pipeline that first scaled and then ran a Logistic Regression on the data. This gave us an initial cross_val_score using 'roc_auc' score of 81.68% and an std of 2%

In the 2nd model, we tried Weight of Evidence Encoder with a combination of LogisticRegression, but this brought our score down to 73%.

Next we used Random Forest, manually playing around with parameters such as criterion: entropy vs gini. Keeping all other  things uniform and just trying the two parameter mentioned, using the same scoring, we got scores of 91.50% with a std of 2.7%.

Always knowing our data was imbalanaced to begin with, we introduced SMOTE to alleviate this, and resampled our training data. Scores jumped up to 96% with an std of 1.8%.

The final model that did well numberwise, was RandomForestClassifier (pretreated with GridSearchCV). We 'asked' GridSearchCV for "best_params". Took those, substituted them in the model and saw a rewarding 98% which we were happy with.

Visuals
Midway in this process, wanting to understand which features carried more weight and importance for problem, we created some visuals to help us identify which features had a higher impact on target. Features seem to have changed depending on how we looked for them. Permutation vs feature importances.

Final takeaways
From our findings, it appears that these customers have a higher risk of churning. Customers who:
1 - have the highest customer service calls
2 - have international plans
3 - are charged the most
4 - use the most minutes

Separately, although we did drop 'state' from our modeling, when exploring our data, it seemed there were some insights that could be taken from it, such as top 5 highest and lowest states to with churning customers.

