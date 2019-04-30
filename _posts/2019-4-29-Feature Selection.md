---
layout:     post
title:      Feature Selection
subtitle:   
date:       2019-4-29
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - Feature Selection, Filter Methods, Wrapper Methods, Embedded Methods
---
### Feature Selection : 

#### Select the features that will help build the most optimum model for the use case. 


### 1. Filter Methods

Filter methods are generally used as a preprocessing step. The selection of features is independent of any machine learning algorithms. Instead, features are selected on the basis of their scores in various statistical tests for their correlation with the outcome variable. The correlation is a subjective term here. Common methods under this category are Pearson’s Correlation, Linear Discriminant Analysis, ANOVA and Chi-Square.

![image](https://cdn-images-1.medium.com/max/1600/1*tcKjpc4Np-9J_dbwoWFDcg.png)

### 2. Wrapper Methods

In wrapper methods, we try to use a subset of features and train a model using them. Based on the inferences that we draw from the previous model, we decide to add or remove features from your subset. The problem is essentially reduced to a search problem. These methods are usually computationally very expensive. Common methods under this category are Forward Selection, Backward Elimination and Recursive Feature Elimination.

![image](https://cdn-images-1.medium.com/max/1600/1*xxx1DZ0UWOY_IwDk76Q9cA.png)

### 3. Embedded Methods

Embedded methods combine the qualities’ of filter and wrapper methods. It’s implemented by algorithms that have their own built-in feature selection methods. LASSO and RIDGE are common ones. 

![image](https://cdn-images-1.medium.com/max/1600/1*MohXtxRJM2QWuNYShpH64w.png)



[Referance](https://towardsdatascience.com/data-science-interview-guide-4ee9f5dc778)