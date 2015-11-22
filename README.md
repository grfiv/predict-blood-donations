# DrivenData's *Predict Blood Donations*

Feature engineering did not improve scores in most cases. Scaling was used for  algorithms that required it. Hyper-parameters were estimated by *GridSearchCV*, a brute-force stratified 10-fold cross-validated search.

**leaderboard_score** is the contest score for predictions of the unknown test-set; lower is better. Camel-case model names refer to scikit-learn models; lower-case were hand-crafted in some way.

|model                      | leaderboard_score|
|:--------------------------|:-----------------:|
|bagged_nolearn             |            0.4313|
|ensemble of averages       |            0.4370|
|voting ensemble            |            0.4396|
|LogisticRegression         |            0.4411|
|bagged_logit               |            0.4442|
|GradientBoostingClassifier |            0.4452|
|LogisticRegressionCV       |            0.4457|
|bagged_scikit_nn           |            0.4465|
|bagged_gbc                 |            0.4527|
|nolearn                    |            0.4566|
|ExtraTreesClassifier       |            0.4729|
|blending ensemble          |            0.4834|
|XGBClassifier              |            0.4851|
|BaggingClassifier          |            0.4885|
|scikit_nn                  |            0.5020|
|boosted_svc                |            0.5334|
|SVC                        |            0.5336|
|SGDClassifier              |            0.5670|
|cosine_similarity          |            0.5732|
|boosted_logit              |            0.5891|
|KMeans                     |            0.6289|
|AdaBoostClassifier         |            0.6642|
|KNeighborsClassifier       |            1.1870|
|RandomForestClassifier     |            1.7907|

Simple logistic regression did quite well; it seems odd that bagging and boosting both reduced its performance. In general though, ensembling did improve performances.

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
-0.17667 -0.07695 -0.00910  0.07141  0.36158

Coefficients:
              Estimate Std. Error t value Pr(>|t|)
(Intercept) -3426.4417  2222.8762  -1.541   0.1492
accuracy     3438.4547  2217.8002   1.550   0.1470
logloss        99.8884    64.3129   1.553   0.1463
f1              1.0221     0.7344   1.392   0.1892
mu            -18.8100     9.1113  -2.064   0.0613 .
std           -41.5887    13.1287  -3.168   0.0081 **
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 0.1481 on 12 degrees of freedom
  (9 observations deleted due to missingness)
Multiple R-squared:  0.8681,	Adjusted R-squared:  0.8132
F-statistic:  15.8 on 5 and 12 DF,  p-value: 6.445e-05
```
Possibly **std** is a stand-in for statistical-learning's **variance**.

--------------------------

The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations) and [BitBucket](https://bitbucket.org/grfiv/predict-blood-donations/). (Only GitHub permits the viewing of IPython notebooks).

Dataset derived from [Blood Transfusion Service Center Data Set](https://archive.ics.uci.edu/ml/datasets/Blood+Transfusion+Service+Center)

<cite>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008 [1]</cite>

[1]:http://dl.acm.org/citation.cfm?id=1498365

<cite>T. Santhanam and Shyam Sundaram , "Application of CART Algorithm in Blood Donors Classification", Journal of Computer Science 6 (5): 548-552, 2010  [2]</cite>

[2]:http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.8749&rep=rep1&type=pdf
