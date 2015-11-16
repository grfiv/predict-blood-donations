# DrivenData's *Predict Blood Donations*

Feature engineering did not improve scores in most cases. Scaling was used for those algorithms that called for it. Hyper-parameters were estimated by *GridSearchCV*, a brute-force stratified 10-fold cross-validated search of parameters.

**leaderboard_score** is the contest score for predictions of the the unknown test-set; lower is better. Camel-case model names refer to built-in scikit-learn models; lower-case were hand-crafted.

|model                      | leaderboard_score|
|:--------------------------|:-----------------:|
|LogisticRegression         |            0.4411|
|GradientBoostingClassifier |            0.4452|
|LogisticRegressionCV       |            0.4457|
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
|bagged_gbc                 |                NA|
|boosted_svc                |                NA|
|bagged_nolearn             |                NA|
|bagged_logit               |                NA|
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
-0.246576 -0.066364 -0.004653  0.067846  0.271408

Coefficients:
              Estimate Std. Error t value Pr(>|t|)  
(Intercept) -7454.1877  3419.8922  -2.180   0.0721 .
accuracy     7439.8570  3422.1310   2.174   0.0727 .
logloss       216.3608    98.9711   2.186   0.0715 .
AUC             9.1473     3.3393   2.739   0.0338 *
mu              2.9374     0.8905   3.298   0.0164 *
std           -11.4574     5.0678  -2.261   0.0645 .
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.1975 on 6 degrees of freedom
  (10 observations deleted due to missingness)
Multiple R-squared:  0.8708,	Adjusted R-squared:  0.7632
F-statistic:  8.09 on 5 and 6 DF,  p-value: 0.01214
```

The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations)

Dataset derived from [Blood Transfusion Service Center Data Set](https://archive.ics.uci.edu/ml/datasets/Blood+Transfusion+Service+Center)

<cite>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008 [1]</cite>

[1]:http://dl.acm.org/citation.cfm?id=1498365

<cite>T. Santhanam and Shyam Sundaram , "Application of CART Algorithm in Blood Donors Classification", Journal of Computer Science 6 (5): 548-552, 2010  [2]</cite>

[2]:http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.8749&rep=rep1&type=pdf
