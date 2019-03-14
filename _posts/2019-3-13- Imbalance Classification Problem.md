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

### Approach to handling Imbalanced Datasets

### 1. Data Level approach: Resampling Techniques

#### 1.1 Random Under-Sampling

Random Undersampling aims to balance class distribution by randomly eliminating majority class examples.  This is done until the majority and minority class instances are balanced out.

**Disadvantages**:

It can discard potentially useful information which could be important for building rule classifiers.
The sample chosen by random under sampling may be a biased sample. And it will not be an accurate representative of the population.

#### 1.2 Random Over-Sampling

Over-Sampling increases the number of instances in the minority class by randomly replicating them in order to present a higher representation of the minority class in the sample.

- **Advantages**
Unlike under sampling this method leads to no information loss.
Outperforms under sampling.

- **Disadvantages**
It increases the likelihood of overfitting since it replicates the minority class events.

#### 1.3 Cluster-Based Over Sampling

#### 1.4  Informed Over Sampling: Synthetic Minority Over-sampling Technique (SMOTE)

#### 1.5 Modified synthetic minority oversampling technique (MSMOTE)

### 2. Algorithmic Ensemble Techniques

#### 2.1 Bagging 

#### 2.2 Boosting

####



In most cases, synthetic techniques like SMOTE and MSMOTE will outperform the conventional oversampling and undersampling methods.

For better results, one can use synthetic sampling methods like SMOTE and MSMOTE along with advanced boosting methods like Gradient boosting and XG Boost.