# DrivenData's *Predict Blood Donations*

Feature engineering did not improve scores in most cases. Scaling was used for  algorithms that required it. Hyper-parameters were estimated by *GridSearchCV*, a brute-force stratified 10-fold cross-validated search.

**leaderboard_score** is the contest score for predictions of the the unknown test-set; lower is better. Camel-case model names refer to scikit-learn models; lower-case were hand-crafted in some way.

|model                      | leaderboard_score|
|:--------------------------|:-----------------:|
|bagged_nolearn             |            0.4313|
|LogisticRegression         |            0.4411|
|voting_ensemble_soft       |            0.4415|
|bagged_logit               |            0.4442|
|GradientBoostingClassifier |            0.4452|
|LogisticRegressionCV       |            0.4457|
|bagged_scikit_nn           |            0.4465|
|bagged_gbc                 |            0.4527|
|nolearn                    |            0.4566|
|ExtraTreesClassifier       |            0.4729|
|XGBClassifier              |            0.4851|
|BaggingClassifier          |            0.4885|
|ensemble of averages       |            0.4896|
|SVC                        |            0.5336|
|SGDClassifier              |            0.5670|
|cosine_similarity          |            0.5732|
|KMeans                     |            0.6289|
|AdaBoostClassifier         |            0.6642|
|boosted_logit              |            0.6891|
|KNeighborsClassifier       |            1.1870|
|RandomForestClassifier     |            1.7907|
|voting_ensemble_hard       |                NA|
|boosted_svc                |                NA|
|scikit_nn                  |                NA|


A number of statistics were recorded for each model from 10-fold CV predictions of the training data:   
  * **accuracy**  the proportion correctly predicted
  * **logloss**  the *sklearn.metrics.log_loss*
  * **AUC**  the area under the ROC curve
  * **f1**   the weighted average of precision and recall
  * **mu** the average over 100 cross-validated scores with permutations
  * **std** the stdev over 100 cross-validated scores with permutations

Starting with all the variables, R's *step* function produced the following
```
Call:
lm(formula = leaderboard_score ~ mu + std, data = score_data,
    na.action = na.omit)

Residuals:
     Min       1Q   Median       3Q      Max
-0.19593 -0.05939 -0.04488  0.00603  0.42108

Coefficients:
            Estimate Std. Error t value Pr(>|t|)
(Intercept)   25.602      3.271   7.827 2.84e-06 ***
mu           -32.920      4.306  -7.645 3.66e-06 ***
std          -60.331      8.667  -6.961 9.90e-06 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.165 on 13 degrees of freedom
  (8 observations deleted due to missingness)
Multiple R-squared:  0.8211,	Adjusted R-squared:  0.7936
F-statistic: 29.84 on 2 and 13 DF,  p-value: 1.386e-05
```

The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations) and [BitBucket](https://bitbucket.org/grfiv/predict-blood-donations/)

Dataset derived from [Blood Transfusion Service Center Data Set](https://archive.ics.uci.edu/ml/datasets/Blood+Transfusion+Service+Center)

<cite>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008 [1]</cite>

[1]:http://dl.acm.org/citation.cfm?id=1498365

<cite>T. Santhanam and Shyam Sundaram , "Application of CART Algorithm in Blood Donors Classification", Journal of Computer Science 6 (5): 548-552, 2010  [2]</cite>

[2]:http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.8749&rep=rep1&type=pdf
