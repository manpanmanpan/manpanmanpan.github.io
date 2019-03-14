---
layout:     post
title:      Imbalance Classification Problem
subtitle:    
date:       2019-3-13
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - 
---

### Imbalance Classification Example:

- Fraud detection

- Datasets to identify customer churn where a vast majority of customers will continue using the service. Specifically, Telecommunication companies where Churn Rate is lower than 2 %.

- Data sets to identify rare diseases in medical diagnostics etc.

- Natural Disaster like Earthquakes


### 1. Metrics

Generally, this problem deals with the trade-off between recall (percent of truly positive instances that were classified as such) and precision (percent of positive classifications that are truly positive). In situations where we want to detect instances of a minority class, we are usually concerned more so with **recall** than precision, as in the context of detection, it is usually more costly to miss a positive instance than to falsely label a negative instance. Thus, when comparing approaches to imbalanced classification problems, consider using metrics beyond accuracy such as recall, precision, F1 Score and AUC-ROC.


### 2. Cost-sensitive Learning

Cost-sensitive learning changes this, and uses a function C(p, t) that specifies the cost of misclassifying an instance of class t as class p. This allows us to penalize misclassifications of the minority class more heavily than we do with misclassifications of the majority class, in hopes that this increases the true positive rate. A common scheme for this is to have the cost equal to the inverse of the proportion of the data-set that the class makes up. This increases the penalization as the class size decreases.

### 3. Resampling Techniques

#### 3.1 Under-Sampling / Over-Sampling

Oversampling the minority can lead to model overfitting, since it will introduce duplicate instances, drawing from a pool of instances that is already small. Similarly, undersampling the majority can end up leaving out important instances that provide important differences between the two classes.

#### 3.2 Informed Over Sampling: Synthetic Minority Over-sampling Technique (SMOTE)

SMOTE, which actually creates new instances of the minority class by forming convex combinations of neighboring instances. As the graphic below shows, it effectively draws lines between minority points in the feature space, and samples along these lines. This allows us to balance our data-set without as much overfitting, as we create new synthetic examples rather than using duplicates. This however does not prevent all overfitting, as these are still created from existing data points.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552539750(1).jpg?raw=true)


### 4. Anomaly Detection

In **more extreme** cases, it may be better to think of classification under the context of anomaly detection. In anomaly detection, we assume that there is a “normal” distribution(s) of data-points, and anything that sufficiently deviates from that distribution(s) is an anomaly. When we reframe our classification problem into an anomaly detection problem, we treat the majority class as the “normal” distribution of points, and the minority as anomalies. There are many algorithms for anomaly detection such as clustering methods, One-class SVMs, and Isolation Forests.

### 5. Algorithmic Ensemble Techniques (Bagging / Boosting)

### Conclusion

- Simple sampling techniques may overcome slight imbalance, whereas anomaly detection methods may be required for extreme imbalances.

- In most cases, synthetic techniques like SMOTE  will outperform the conventional oversampling and undersampling methods.

- For better results, we can use synthetic sampling methods like SMOTE along with advanced boosting methods like Gradient boosting and XG Boost.