---
layout:     post
title:      Tree Model
subtitle:   Decision Tree, Random Forest, Bagging, Boosting
date:       2019-3-11
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - ID3, C4.5, CART, Adaboosting, Gradient Boosting, Random Forest
---


## 1. Decision Tree

### 1.1 ID3 

### 1.2 C4.5

### 1.3. CART

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552342459(1).jpg?raw=true)


## 2. Bagging

We bootstrap, by taking repeated samples from the (single) training data set. In this approach we generate B different bootstrapped training data sets. We then train our method on the bth bootstrapped training set in order to get $\hat{f}^{*b}(x)$, and finally average all the predictions, to obtain:

$$ \hat{f_{bag}(x)} = \frac{1}{B}\sum_{b=1}^B\hat{f}^{*b}(x) $$

This is called bagging.

### 2.2 Out-of-Bag Error Estimation

For Example, each bagged tree makes use of around two-thirds of the observations. The remaining one-third of the observations not used to fit a given bagged tree are referred to as the out-of-bag (OOB) observations.

The resulting OOB error is a valid estimate of the test error for the bagged model, since the response for each observation is predicted using only the trees that were not fit using that observation. With B sufficiently large, OOB error is virtually equivalent to leave-one-out cross-validation error. The OOB approach for estimating the test error is particularly convenient when performing bagging on large data sets for which cross-validation would be computationally onerous.

## 3. Random Forests

Random forests provide an improvement over bagged trees by way of a random small tweak that decorrelates the trees.

Each time a split in a tree is considered, a random sample of m predictors is chosen as split candidates from the full set of p predictors. The split is allowed to use only one of those m predictors. A fresh sample of
m predictors is taken at each split, and typically we choose $ m ≈ \sqrt{p} $

#### Why Random Forests?

Suppose that there is one very strong predictor in the data set, along with a number of other moderately strong predictors. Then in the collection of bagged trees, most or all of the trees will use this strong predictor in the top split.
Consequently, all of the bagged trees will look quite similar to each other.
Hence the predictions from the bagged trees will be highly correlated. Unfortunately, averaging many highly correlated quantities does not lead to
as large of a reduction in variance as averaging many uncorrelated quantities.
Random forests overcome this problem by forcing each split to consider only a subset of the predictors.

As with bagging, random forests will not overfit if we increase
B, so in practice we use a value of B sufficiently large for the error rate to
have settled down.