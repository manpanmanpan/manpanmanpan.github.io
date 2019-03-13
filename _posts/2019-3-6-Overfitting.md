---
layout:     post
title:      Overfitting
subtitle:   Regularization, Cross Validation, Lasso, Ridge
date:       2019-3-6
author:     Cassie Pan
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Regularization, Cross Validation, Lasso, Ridge
---

### Overfitting

#### Cross Validation


- **Holdout Method**

  Removing a part of the training data and using it to get predictions from the model trained on rest of the data.
  It still suffers from issues of high variance. This is because it is not certain which data points will end up in the validation set and the result might be entirely different for different sets.

- **K-Fold Cross Validation**

  In K Fold cross validation, the data is divided into k subsets. Now the holdout method is repeated k times, such that each time, one of the k subsets is used as the test set/ validation set and the other k-1 subsets are put together to form a training set. The error estimation is averaged over all k trials to get total effectiveness of our model. As can be seen, every data point gets to be in a validation set exactly once, and gets to be in a training set k-1 times. This significantly reduces bias as we are using most of the data for fitting, and also significantly reduces variance as most of the data is also being used in validation set. As a general rule and empirical evidence, K = 5 or 10 is generally preferred.

- **Stratified K-Fold Cross Validation**

  In some cases, a large imbalance in the response variables. 
  For example, in dataset concerning price of houses, there might be large number of houses having high price. 
  Or in case of classification, there might be several times more negative samples than positive samples. 
  For such problems, a slight variation in the K Fold cross validation technique is made, such that each fold contains approximately the same percentage of samples of each target class as the complete set, or in case of prediction problems, the mean response value is approximately equal in all the folds. This variation is also known as Stratified K Fold.

- **Leave-P-Out Cross Validation**

  This approach leaves p data points out of training data, i.e. if there are n data points in the original sample then, n-p samples are used to train the model and p points are used as the validation set. This is repeated for all combinations in which original sample can be separated this way, and then the error is averaged for all trials,to give overall effectiveness.


  This method is exhaustive in the sense that it needs to train and validate the model for all possible combinations, and for moderately large p, it can become computationally infeasible.


  So we always let p = 1. This is known as Leave one out cross validation. This case, the number of possible combinations is equal to number of data points in original sample or n.

#### Regularization

Regularization, significantly reduces the variance of the model, without substantial increase in its bias.

[Regularization](https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a)

This is a form of regression, that constrains/ regularizes or shrinks the coefficient estimates towards zero. In other words, this technique discourages learning a more complex or flexible model, so as to avoid the risk of overfitting.

- Ridge Regression (L2 norm)

$$ \sum_{i=1}^n (y_i - \beta_0 - \sum_{j=1}^p\beta_jX_{ij})^2 + \lambda\sum_{j=1}^p\beta_j^2$$

  The coefficients are estimated by minimizing this function. Here, λ is the tuning parameter that decides how much we want to penalize the flexibility of our model. We shrink the estimated association of each variable with the response, except the intercept β0, This intercept is a measure of the mean value of the response when $x_{i1} = x_{i2} = …= x_{ip} = 0$.


  When λ = 0, the penalty term has no eﬀect, and the estimates produced by ridge regression will be equal to least squares. However, as λ→∞, the impact of the shrinkage penalty grows, and the ridge regression coeﬃcient estimates will approach zero.


  We need to standardize the predictors or bring the predictors to the same scale before performing ridge regression.


  Disadvantage of ridge regression, which is model interpretability. It will shrink the coefficients for least important predictors, very close to zero. But it will never make them exactly zero. In other words, the final model will include all predictors. 

- Lasso (L1 norm)

$$ \sum_{i=1}^n (y_i - \beta_0 - \sum_{j=1}^p\beta_jX_{ij})^2 + \lambda\sum_{j=1}^p|\beta_j|$$

This variation differs from ridge regression only in penalizing the high coefficients.

- Constraint functions

Consider their are 2 parameters in a given problem. Then according to above formulation, the ridge regression is expressed by $β_1² + β_2² ≤ S$. This implies that ridge regression coefficients have the smallest RSS(loss function) for all points that lie within the circle given by $β_1² + β_2² ≤ S$.


Similarly, for lasso, the equation becomes,$\|β_1\|+\|β_2\|≤ S$.
This implies that lasso coefficients have the smallest RSS(loss function) for all points that lie within the diamond given by $\|β_1\|+\|β_2\|≤ S$.



![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551741185(1).jpg?raw=true)


The above image shows the constraint functions(green areas), for lasso(left) and ridge regression(right), along with contours for RSS(red ellipse).


Since ridge regression has a circular constraint with no sharp points, this intersection will not generally occur on an axis, and so the ridge regression coeﬃcient estimates will be exclusively non-zero. However, the lasso constraint has corners at each of the axes, and so the ellipse will often intersect the constraint region at an axis. When this occurs, one of the coeﬃcients will equal zero. In higher dimensions(where parameters are much more than 2), many of the coeﬃcient estimates may equal zero simultaneously.


The tuning parameter $\lambda$, used in the regularization techniques described above, controls the impact on bias and variance. As the value of $\lambda$ rises, it reduces the value of coefficients and thus reducing the variance. Till a point, this increase in $\lambda$ is beneficial as it is only reducing the variance(hence avoiding overfitting), without loosing any important properties in the data. But after certain value, the model starts loosing important properties, giving rise to bias in the model and thus underfitting. Therefore, the value of $\lambda$ should be carefully selected.


#### What are the pros & cons of each of L1 / L2 regularization?

- L1 regularization can't help with multicollinearity. It will just pick the feature with the largest correlation to the outcome (which isn't useful if you have an interest in estimating coefficients for all features which are strongly correlated with your target). L1 help with feature selection.

- L2 regularization can't help with feature selection, but it help with multicollinearity. 