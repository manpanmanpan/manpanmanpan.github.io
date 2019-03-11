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

We bootstrap, by taking repeated samples from the (single) training data set. In this approach we generate B different bootstrapped training data sets. We then train our method on the bth bootstrapped training set in order to get $\hat{f^{*b}(x)}$, and finally average all the predictions, to obtain:

$$ \hat{f_{bag}(x)} = \frac{1}{B}\sum_{b=1}^B\hat{f^{*b}(x)} $$

This is called bagging.