---
layout:     post
title:      How to evaluate model performance
subtitle:   F1 score, ROC, AUC, Recall, Precision, Log-Loss
date:       2019-3-11
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    -  F1 score, ROC, AUC, Recall, Precision, Log-Loss
---

### How to evaluate model performance?

### Definition:

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552427573(1).png?raw=true)

#### Recall or Sensitivity or TPR (True Positive Rate):

Number of items correctly indentified as positive out of total true positive - $\frac{TP}{TP + FN}$

#### Precision: 

Number of items correctly indentified as positive out of total items identified as positive - $\frac{TP}{TP+FP}$

#### Specificity or TNR (True Negative Rate):

Number of items correctly identified as negative out of total negatives - $\frac{TN}{TN+FP}$

#### False Positive Rate or Type I error:

Number of items wrongly identified as positive out of total true negatives - $\frac{FP}{FP+TN}$

#### False Negative Rate or Type II error:

Number of items wrongly identified as negative out of total true positives - $\frac{FN}{FN+TP}$

#### F1 Score:

It is a harmonic mean of precision and recall given by- 
$F1 = \frac{2*Precision*Recall}{Precision + Recall}$


### 1. Precision，Recall，F1 Score

**Recall**: ability of a classification model to identify all relevant instances.

**Precision**: ability of a classification model to return only relevant instances.

**F1 score**: single metric that combines recall and precision using the harmonic mean.

$$The ~~Precision ~~and ~~Recall~~ Trade-off$$

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552434268(1).jpg?raw=true)

#### Why F1 Score?

In cases where we want to find an optimal blend of precision and recall we can combine the two metrics using what is called the F1 score.

**Note**: We use the harmonic mean instead of a simple average because it punishes **extreme values**. F1 Score is sensitive to threshold value.


#### When is precision more important?

For YouTube recommendations, false-negatives is less of a concern. Precision is better here.

####  When is recall more important?

For rare cancer data modeling, anything that doesn't account for false-negatives is a crime. Recall is a better measure than precision.

Also, in preliminary disease screening of patients for follow-up examinations, we would probably want a recall near 1.0.

- We want to find all patients who actually have the disease 

- And we can accept a low precision if the cost of the follow-up examination is not significant.


The major difference is FP vs FN. YouTube recommendation don't place emphasis on FN but hospital clinical decisions must.
Which is more important simply depends on what the costs of each error is.

[Beyond Accuracy: Precision and Recall](https://towardsdatascience.com/beyond-accuracy-precision-and-recall-3da06bea9f6c)

### 2. ROC - AUC

- Receiver operating characteristic (ROC) curve: plots the true positive rate (TPR) versus the false positive rate (FPR) as a function of the model’s threshold for classifying a positive

- Area under the curve (AUC): metric to calculate the overall performance of a classification model based on area under the ROC curve

Receiver Operating Characteristic (ROC) curve shows how the recall vs precision relationship changes as we vary the threshold for identifying a positive in our model. The threshold represents the value above which a data point is considered in the positive class. By altering the threshold, we can try to achieve the right precision vs recall balance.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552448521(1).png?raw=true)

- Plots out the sensitivity and specificity for every possible decision rule cutoff between 0, 1.

- X - axis: 1 - specificity (= false positive fraction = $\frac{FP}{FP+TN}$).

- Y - axis: sensitivity (=true positive fraction = $\frac{TP}{YP+FN}$).

- The best decision rule is high on recall/sensitivity (Y) and low on 1-specificity(X).

- ROC-AUC score is independent of the threshold set for classification because it only considers the rank of each prediction and not its absolute value. The same is not true for F1 score which needs a threshold value in case of probabilities output.

- When AUC is 0.7, it means there is 70% chance that model will be able to distinguish between positive class and negative class.

### 3. Log-Loss

Log-loss is a measurement of accuracy that incorporates the idea of probabilistic confidence given by following expression for binary class:

$$ -(ylog(p)+(1-y)log(1-p))$$

y = true label, p = predicted prob

It takes into account the uncertainty of your prediction based on how much it varies from the actual label. In the worst case,let’s say you predicted 0.5 for all the observations. So log-loss will become -log(0.5) = 0.69. Hence, we can say that anything above 0.69 is a very poor model considering the actual probabilities.


[Choosing the Right Metric for Evaluating Machine Learning Models](https://medium.com/usf-msds/choosing-the-right-metric-for-evaluating-machine-learning-models-part-2-86d5649a5428)

#### Some tricks from the above link:

For Balanced data:

- If you care for absolute probabilistic difference, go with log-loss.

- If you care only for the final class prediction and you don’t want to tune threshold, go with AUC score.

- F1 score is sensitive to threshold and you would want to tune it first before comparing the models.

For Imbalanced data:

- log-loss function is symmetric and does not differentiate between classes, so log-loss is failing in imbalanced case.

- If you care for a class which is smaller in number independent of the fact whether it is positive or negative, go for ROC-AUC score.

- When you have a small positive class, then F1 score makes more sense. This is the common problem in **fraud / spam mail  detection** where positive labels are few.