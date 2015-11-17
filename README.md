# DrivenData's *Predict Blood Donations*

Feature engineering did not improve scores in most cases. Scaling was used for those algorithms that called for it. Hyper-parameters were estimated by *GridSearchCV*, a brute-force stratified 10-fold cross-validated search of parameters.

**leaderboard_score** is the contest score for predictions of the the unknown test-set; lower is better. Camel-case model names refer to built-in scikit-learn models; lower-case were hand-crafted.

|model                      | leaderboard_score|
|:--------------------------|:----------------:| 
|bagged_nolearn             |            0.4313|
|LogisticRegression         |            0.4411|
|bagged_logit               |            0.4442|
|GradientBoostingClassifier |            0.4452|
|LogisticRegressionCV       |            0.4457|
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
|KNeighborsClassifier       |            1.1870|
|RandomForestClassifier     |            1.7907|
|voting_ensemble_hard       |                NA|
|voting_ensemble_soft       |                NA|
|boosted_svc                |                NA|
|boosted_logit              |                NA|

*
A number of statistics were recorded for each model using 10-fold CV predictions of the training data:
  * **accuracy**  the proportion of the training set folds correctly predicted
  * **logloss**  the *sklearn.metrics.log_loss* on the training set predictions
    (the contest-specified formula produced identical results)  
  * **AUC**  the area under the ROC curve
  * **f1**   the weighted average of precision and recall
  * **mu** the average over 100 cross-validated scores with permutations
  * **std** the stdev over 100 cross-validated scores with permutations

R's *step* function produced the following
```
Call:
lm(formula = leaderboard_score ~ accuracy + logloss + AUC + mu +
    std, data = score_data, na.action = na.omit)

Residuals:
      Min        1Q    Median        3Q       Max
-0.275512 -0.029650 -0.001879  0.084887  0.265253

Coefficients:
              Estimate Std. Error t value Pr(>|t|)
(Intercept) -6127.1978  2808.5613  -2.182  0.06071 .
accuracy     6112.6970  2810.1455   2.175  0.06132 .
logloss       177.9199    81.2793   2.189  0.06002 .
AUC             9.6952     2.8267   3.430  0.00896 **
mu              2.9213     0.7899   3.698  0.00606 **
std           -11.5539     4.7100  -2.453  0.03975 *
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.1897 on 8 degrees of freedom
  (8 observations deleted due to missingness)
Multiple R-squared:  0.8488,	Adjusted R-squared:  0.7543
F-statistic: 8.982 on 5 and 8 DF,  p-value: 0.003888
```

The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations)

Dataset derived from [Blood Transfusion Service Center Data Set](https://archive.ics.uci.edu/ml/datasets/Blood+Transfusion+Service+Center)

<cite>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008 [1]</cite>

[1]:http://dl.acm.org/citation.cfm?id=1498365

<cite>T. Santhanam and Shyam Sundaram , "Application of CART Algorithm in Blood Donors Classification", Journal of Computer Science 6 (5): 548-552, 2010  [2]</cite>

[2]:http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.8749&rep=rep1&type=pdf
