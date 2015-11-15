# DrivenData's *Predict Blood Donations*

Feature engineering did not improve scores in most cases. Scaling was used for those algorithms that called for it. Hyper-parameters were estimated by *GridSearchCV*, a brute-force stratified 10-fold cross-validated search of parameters. Camel-case model names refer to built-in scikit-learn models; lower-case were hand-crafted.

* **score** is the leaderboard score for the test-set predictions
    * **accuracy** is the proportion of the training set correctly predicted
    * **logloss** is the *sklearn.metrics.log_loss* on the training set;
      the contest-specified formula produced identical results.  
    * **AUC** is the area under the ROC curve
    * **f1**  is the weighted average of precision and recall

None of the training metrics were predictive of **score**; R's *step* function chose **AUC** and **f1** but with p>0.12 and  Adjusted R^2 of 0.2387.




|model                      |  score | accuracy| logloss|    AUC|     f1|
|:--------------------------|:------:|--------:|-------:|------:|------:|
|GradientBoostingClassifier | 0.4452|   0.8177|  6.2962| 0.6717| 0.5070|
|nolearn                    | 0.4566|   0.8056|  6.7159| 0.6711| 0.5044|
|ExtraTreesClassifier       | 0.4729|   0.8402|  5.5467| 0.7100| 0.5806|
|XGBClassifier              | 0.4851|   0.8420|  5.4567| 0.7100| 0.5806|
|BaggingClassifier          | 0.4885|   0.8507|  5.1568| 0.7107| 0.5865|
|ensemble of averages       | 0.4896|       NA|      NA|     NA|     NA|
|SVC                        | 0.5336|   0.9375|  2.1587| 0.8745| 0.8525|
|SGDClassifier              | 0.5670|   0.7500|  8.6348| 0.6545| 0.4745|
|cosine_similarity          | 0.5732|   0.7906|  7.2333| 0.6452| 0.4595|
|AdaBoostClassifier         | 0.6642|   0.8090|  6.5960| 0.6635| 0.4907|
|KNeighborsClassifier       | 1.1870|   0.8142|  6.4161| 0.6620| 0.4880|
|RandomForestClassifier     | 1.7907|   0.9184|  2.8183| 0.8520| 0.8097|
|KMeans                     |     NA|   0.7326|  9.2324| 0.5636| 0.3000|
|LogisticRegression         |     NA|   0.7760|  7.7353| 0.5649| 0.2543|
|LogisticRegressionCV       |     NA|   0.7830|  7.4954| 0.5794| 0.2938|


The work is available on [GitHub](https://github.com/grfiv/predict-blood-donations)
