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
|scikit_nn                  |            0.5020|
|SVC                        |            0.5336|
|SGDClassifier              |            0.5670|
|cosine_similarity          |            0.5732|
|boosted_logit              |            0.5891|
|KMeans                     |            0.6289|
|AdaBoostClassifier         |            0.6642|
|KNeighborsClassifier       |            1.1870|
|RandomForestClassifier     |            1.7907|
|voting_ensemble_hard       |                NA|
|boosted_svc                |                NA|

It seems ironic that that simple logistic regression did so well and odd that neither bagging nor boosting improved its performance.

------------------------------

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
lm(formula = leaderboard_score ~ accuracy + logloss + f1 + mu +
    std, data = score_data, na.action = na.omit)

Residuals:
     Min       1Q   Median       3Q      Max
-0.19483 -0.07857 -0.01207  0.03450  0.36601

Coefficients:
             Estimate Std. Error t value Pr(>|t|)  
(Intercept) -2707.589   2152.885  -1.258   0.2346  
accuracy     2716.710   2148.005   1.265   0.2321  
logloss        79.103     62.286   1.270   0.2303  
f1              1.702      1.036   1.643   0.1287  
mu            -16.433     10.135  -1.621   0.1332  
std           -39.776     13.952  -2.851   0.0158 *
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.1508 on 11 degrees of freedom
  (7 observations deleted due to missingness)
Multiple R-squared:  0.8742,	Adjusted R-squared:  0.8171
F-statistic: 15.29 on 5 and 11 DF,  p-value: 0.0001241
```
Possibly **std** is a stand-in for statistical-learning's **variance**.

--------------------------

The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations) and [BitBucket](https://bitbucket.org/grfiv/predict-blood-donations/)

Dataset derived from [Blood Transfusion Service Center Data Set](https://archive.ics.uci.edu/ml/datasets/Blood+Transfusion+Service+Center)

<cite>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008 [1]</cite>

[1]:http://dl.acm.org/citation.cfm?id=1498365

<cite>T. Santhanam and Shyam Sundaram , "Application of CART Algorithm in Blood Donors Classification", Journal of Computer Science 6 (5): 548-552, 2010  [2]</cite>

[2]:http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.8749&rep=rep1&type=pdf
