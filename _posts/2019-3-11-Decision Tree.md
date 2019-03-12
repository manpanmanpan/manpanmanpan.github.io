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

#### Advantages and Disadvantages of Trees

▲ Easier to explain 

▲ More closely mirror humanndecision-making 

▲ Trees can be displayed graphically, and are easily interpreted

▲ Trees can easily handle qualitative predictors without the need to create dummy variables

▼ Unfortunately, trees generally do not have the same level of predictive accuracy as some of the other regression and classification approaches

▼ Additionally, trees can be very non-robust. A small change in the data can cause a large change in the final estimated tree


## 2. Bagging

We bootstrap, by taking repeated samples from the (single) training data set. In this approach we generate B different bootstrapped training data sets. We then train our method on the $b_th$ bootstrapped training set in order to get $\hat{f}^{*b}(x)$, and finally average all the predictions, to obtain:

$$ \hat{f}_{bag}(x) = \frac{1}{B}\sum_{b=1}^B\hat{f}^{*b}(x) $$

This is called bagging. Each tree is built on a bootstrap data set, independent of the other trees. The number of trees B is not a critical parameter with bagging; Using a very large value of B will **not lead to overfitting**.

### 2.2 Out-of-Bag Error Estimation

For Example, each bagged tree makes use of around two-thirds of the observations. The remaining one-third of the observations not used to fit a given bagged tree are referred to as the out-of-bag (OOB) observations.

The resulting OOB error is a valid estimate of the test error for the bagged model, since the response for each observation is predicted using only the trees that were not fit using that observation. With B sufficiently large, OOB error is virtually equivalent to leave-one-out cross-validation error. The OOB approach for estimating the test error is particularly convenient when performing bagging on large data sets for which cross-validation would be computationally onerous.

#### Any pros and cons in practical implementation?


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

As with bagging, random forests will **not overfit** if we increase B.


#### Any pros and cons in practical implementation?


## 4. Boosting

Boosting works in a similar way as Bagging, except that the trees are grown sequentially: each tree is grown using information from previously grown trees. Boosting does not involve bootstrap sampling; instead each
tree is fit on a modified version of the original data set.

Note that in boosting, the construction of each tree depends strongly on the trees that have already been grown.

In boosting, because the growth of a particular tree takes into account the other trees that have already been grown, smaller trees are typically sufficient. Using smaller trees can **aid in interpretability** as well; for instance, using stumps leads to an **additive** model.

### 4.1 AdaBoosting

### 4.2 Gradient Boosting


#### Any pros and cons in practical implementation?

 