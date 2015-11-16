# DrivenData's *Predict Blood Donations*

Feature engineering did not improve scores in most cases. Scaling was used for those algorithms that called for it. Hyper-parameters were estimated by *GridSearchCV*, a brute-force stratified 10-fold cross-validated search of parameters. Camel-case model names refer to built-in scikit-learn models; lower-case were hand-crafted.

* **score** is the leaderboard score for the test-set predictions
    * **accuracy** is the proportion of the training set correctly predicted
    * **logloss** is the *sklearn.metrics.log_loss* on the training set   
      (the contest-specified formula produced identical results)  
    * **AUC** is the area under the ROC curve
    * **f1**  is the weighted average of precision and recall

None of the training metrics were predictive of **score**; R's *step* function chose **logloss** but with p>0.15 and  Adjusted R^2 of 0.09271.




|model                      |  score| accuracy| logloss|    AUC|     f1|
|:--------------------------|------:|--------:|-------:|------:|------:|
|LogisticRegression         | 0.4411|   0.7760|  7.7353| 0.5649| 0.2543|
|GradientBoostingClassifier | 0.4452|   0.8177|  6.2962| 0.6717| 0.5070|
|LogisticRegressionCV       | 0.4457|   0.7830|  7.4954| 0.5794| 0.2938|
|nolearn                    | 0.4566|   0.8056|  6.7159| 0.6711| 0.5044|
|ExtraTreesClassifier       | 0.4729|   0.8402|  5.5467| 0.7100| 0.5806|
|XGBClassifier              | 0.4851|   0.8420|  5.4567| 0.7100| 0.5806|
|BaggingClassifier          | 0.4885|   0.8507|  5.1568| 0.7107| 0.5865|
|ensemble of averages       | 0.4896|       NA|      NA|     NA|     NA|
|SVC                        | 0.5336|   0.9375|  2.1587| 0.8745| 0.8525|
|SGDClassifier              | 0.5670|   0.7500|  8.6348| 0.6545| 0.4745|
|cosine_similarity          | 0.5732|   0.7906|  7.2333| 0.6452| 0.4595|
|KMeans                     | 0.6289|   0.7326|  9.2324| 0.5636| 0.3000|
|AdaBoostClassifier         | 0.6642|   0.8090|  6.5960| 0.6635| 0.4907|
|KNeighborsClassifier       | 1.1870|   0.8142|  6.4161| 0.6620| 0.4880|
|RandomForestClassifier     | 1.7907|   0.9184|  2.8183| 0.8520| 0.8097|
|voting_ensemble_hard       |     NA|   0.8177|  6.2962| 0.6618| 0.4878|
|voting_ensemble_soft       |     NA|   0.8177|  6.2962| 0.6618| 0.4878|
|bagged_gbc                 |     NA|   0.8108|  6.5360| 0.6572| 0.4785|
|boosted_svc                |     NA|   0.7813|  7.5554| 0.5435| 0.1600|
|bagged_nolearn             |     NA|   0.7986|  6.9558| 0.6467| 0.4579|

The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations)

Dataset derived from [Blood Transfusion Service Center Data Set](https://archive.ics.uci.edu/ml/datasets/Blood+Transfusion+Service+Center)

<cite>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008 [1]</cite>

[1]:http://dl.acm.org/citation.cfm?id=1498365

<cite>T. Santhanam and Shyam Sundaram , "Application of CART Algorithm in Blood Donors Classification", Journal of Computer Science 6 (5): 548-552, 2010  [2]</cite>

[2]:http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.8749&rep=rep1&type=pdf
