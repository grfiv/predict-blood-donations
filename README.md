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

It seems ironic that simple logistic regression did so well and odd that neither bagging nor boosting improved its performance.

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
-0.19380 -0.07567 -0.01766  0.04934  0.35870

Coefficients:
              Estimate Std. Error t value Pr(>|t|)  
(Intercept) -3244.0494  2213.1761  -1.466   0.1707  
accuracy     3252.3528  2208.4147   1.473   0.1689  
logloss        94.6258    64.0312   1.478   0.1675  
f1              1.7265     0.9765   1.768   0.1047  
mu            -15.5120     9.5430  -1.625   0.1323  
std           -38.1748    13.4085  -2.847   0.0159 *
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 0.147 on 11 degrees of freedom
  (7 observations deleted due to missingness)
Multiple R-squared:  0.8805,	Adjusted R-squared:  0.8262
F-statistic: 16.21 on 5 and 11 DF,  p-value: 9.453e-05
```
Possibly **std** is a stand-in for statistical-learning's **variance**.

--------------------------

The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations) and [BitBucket](https://bitbucket.org/grfiv/predict-blood-donations/)

Dataset derived from [Blood Transfusion Service Center Data Set](https://archive.ics.uci.edu/ml/datasets/Blood+Transfusion+Service+Center)

<cite>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008 [1]</cite>

[1]:http://dl.acm.org/citation.cfm?id=1498365

<cite>T. Santhanam and Shyam Sundaram , "Application of CART Algorithm in Blood Donors Classification", Journal of Computer Science 6 (5): 548-552, 2010  [2]</cite>

[2]:http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.8749&rep=rep1&type=pdf
