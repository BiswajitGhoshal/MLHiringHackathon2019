# MLHiringHackathon2019
## Approach description

### Approach in brief:-
i. In the training set, out of total 116058 records, only 636 (0.55%) had defaulted – which implied the data is highly-imbalanced.

ii. To have a balanced dataset, I used SMOTE.  For the selected categorical variables (chosen based on their effect on accuracy of outcome prediction), I used corresponding dummy variables.

iii. First I used Random Forest – but that did not give good score.  After that I used XGBClassifier (with tuning various parameters) to build the best model possible – and then used it to predict the test set (after making similar feature engineering).

### Data Processing / Feature Engineering:-
i. To have a balanced dataset, I used SMOTE, before training any model.  If learning was attempted without having some sort of balanced dataset, it would have hardly learnt to predict the defaults.

ii. Initially I tried to model with only the m1, m2, m3….m12 columns, using both Random Forest and XGBoostClassifiers – but the scores were not good enough.

iii. Hence, I used all the columns – except, the financial_institution column (since, it alone would have given 19 dummy-columns.  However, it along with other selected few columns could have been tried (which I could not do due to time constraint).  Also, another consideration was that SMOTE allows maximum 32 columns.  Hence, to get maximum number and types of variables to be included in the model, I accommodated most of the other variables and left out financial_institution column.

iv. Also, I dropped first_payment_date (since it gave less accuracy compared to origination_date), and kept the origination_date.

v. I had dummy-columns for the categorical variables (i.e. source, origination_date and loan_purpose).

### The final model:-
 The final model  is an XGBClassifier with 485 estimators, maximum depth of 2, learning rate of 0.01, 0.6 sub-samples and 0.6 col-samples.  When it was trained on the entire training-set it produced best score for the test-dataset.
How it was arrived:-
i. While training on 75% and validating on remaining 25% of training data, with 1000 estimators , learning rate of 0.1, with maximum depth 2 to 10, the most feasible combination of F1-score, recall and accuracy was found at maximum depth of 2.

ii. Then, I started fine-tuning the number of estimators on the full training-set and checked the combination of the scores, and found that at 485, it was giving best scores for the test data.

iii. Then I fine-tuned the learning rate and the best scores were had at 0.01 learning rate.

iv. Then I fine-tuned the combination of subsample and colsample_bytree (which were 1 by default) and found that it is giving best scores at 0.6 and 0.6 respectively.

Note:-
1. With larger processing power and more time, grid of above mentioned parameter value-combinations could have been made and tried to find even better model.
