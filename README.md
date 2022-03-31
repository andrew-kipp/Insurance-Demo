# Insurance-Demo

## Executive Summary of Classification Exercise 40
Both logistic regression and CatBoost classification models were able to successfully
classify the target variable, y, and with decent performance on the AUC metric.
However, a scoring metric isn’t the only factor to consider when selecting models and
both logistic regression and CatBoost have their trade-offs affecting whether they can or
should be used in different situations.

Logistic regression benefits from having a fairly quick computation time when restricted
to CPUs and a very easily interpretable final model. Each individual feature in the model
can be understood and the impact to probability due to the change in values of one or
more features can be directly calculated. This simplicity can also be a drawback
because the model may never be as powerful as some of the newer tree-based or deep
learning techniques, and new features are expected to have a linear relationship with
the logit of the response variable so any feature transformations or interaction features
must be manually calculated.

CatBoost classification lacks the simplicity of logistic regression so interpreting the final
model is more difficult and the impact of changes to individual features cannot be
directly measured. But, feature importance can be calculated which can give the user
an understanding of which features have the greatest overall impact on predictions, and
with the creation of SHAP values it is possible to interpret how strongly different
features affect an individual prediction. The tradeoff of the increased complexity is that
CatBoost has the potential to create significantly more powerful models than logistic
regression, which is preferred when model interpretability is not a factor in the end goal.
While CatBoost classification is also usually slower than logistic regression on CPUs, it
can take advantage of GPUs which can make it significantly faster for large datasets.
The CatBoost classifier should perform better on the test data because the final score
on the intermediate test data split was 79.5%, which was ~4.7% than logistic regression.
The CatBoost model also has a smaller performance drop between the cross-validation
performance and intermediate test data performance, ~0.9%, compared to the logistic
regression model’s ~1.8%.

| | Mean AUC on Validation Splits | Std Dev AUC on Validation Splits | AUC on Test Set |
| ------------------- | ------ | ------ | ------ |
| CatBoost Classifier | 0.8033 | 0.0027 | 0.7941 |
| Logistic Regression | 0.7660 | 0.0052 | 0.7478 |

While the model performance metrics are useful for comparison when training and
testing, they are not directly relevant to the business. A better way to present them is in
the form of their business impact or lift, whether that is measured by an increase in
revenue or reduction in costs or losses. AUC is also not directly translatable to business
value so it is usually more important to look at the changes in false positives, false
negatives, and true positives, and how the differences between the models for those
metrics translate to cumulative business impact or lift