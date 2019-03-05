---
layout:     post
title:      Statistic Cheat Sheet
subtitle:   Regression
date:       2019-02-27
author:     Cassie Pan
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Regression
---

#### 1. What is P-value?

Assume that you observe a sample value, e.g. $\bar{x}$ = x, p value = probability under H<sub>0</sub> that you observe a sample as extreme as or more extreme than x.
    what constitutes "extreme" depends on the alternative hypothesus.
For instance p value = P( $\bar{x}$ >= x) if H<sub>1</sub> = u > u<sub>0


P-value is the probability of obtaining a result at least as extreme as the current one, assuming that the null hypothesis is true.

For example:
Imagine we did a study comparing a placebo group to a group that received a new blood pressure medication and the mean blood pressure in the treatment group was 20 mm Hg lower than the placebo group. Assuming the null hypothesis is correct the pvalue is the probability that if we repeated the study the observed difference between the group averages would be at least 20.

#### 2.  Power & Type 1 error & Type 2 error

Type 1 Error = incorrectly rejecting the null hypothesis.
Type 2 Error = fail to reject null when you should have rejected the null hypothesis.

Power is the probability of finding a difference between groups if one truly exists. It is the percentage chance that you will be able to reject the null hypothesis if it is really false.

#### 3. Least Square Principle 

Least square principle is to fit the observed data by minimizing the sum of squared vertical deviations.

#### 4. Residuals
![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551495156(1).jpg?raw=true)

#### 5. SSTO &  SSR &  SSE
SSTO = SSR + SSE

Total deviations  (the variation of the observed Yi around their sample mean) can be decomposed into the sum of two items: 
The deviation of observed value around the fitted regression line (residual) and the deviation of fitted value from the mean.

SSR = SSTO - SSE

Is the effect of X in reducing the variation in Y through linear regression. 

SSR is the reduction in uncertainty in predicting Y by utilizing the predictor X through a linear regression model.

#### 6. $R^2$  &  $R_a^2$
$R^2$ = SSR/SSTO = 1 - SSE/SSTO

$R^2$ is the proportional reduction of the total variation in Y by explaining Y using X through a linear regression model.

For example: $R^2$ = .209 ( y child’s height, x parents’ height )
20% of variation in child’s height may be explained by the variation in parents’ height.

Sometimes, nonlinearity pattern shows larger $R^2$ .
Adding more X variables to the model will always increase $R^2$.

$R_a^2$ = 1 - MSE/MSTO = 1 - n-1/n-p * SSE/SSTO  <= $R^2$

$R_a^2$ may become decrease when adding more X variables into the model because the decrease in SSE may be more than offset by the loose of degrees of freedom in SSE.

#### 7. Confidence Interval Interpretation
Confidence interval provides a range of values which is likely to contain the population parameter of interest.

We have 95% confident that the true value is between [L,R]

#### 8. Model diagnostics
##### Assumptions of the simple linear model with normal errors:
######  Linearity of the regression relation  (residual vs predictor variables plot)

###### Normality of the error terms  (QQ plot)

###### Constant variance of error terms
 ( if the residual vs predictor variable plot (or residual vs fitted value plot) shows unequal dispersion along the horizontal xi_s, then this is an indicator of unequal variance)

TESTS OF EQUAL VARIANCE ( Hartley Test, Brown-Forsythe Test, Bartlett Test)

Unequal error variance remedial measures: Transformation of observation variable Y, ex, BOX-COX procedure; Weighted least squares.

###### Independence of the error terms  
(if measurements are obtained in a time/space sequence, a residual sequence plot can be used to check whether the error terms are serially correlated)

#### 9. Regression and Causation 
Regression analysis by itself doesn’t imply cause and effect relation
A strong regression relation neither implies ‘X causes Y’ nor implies ‘Y causes X’. It only means that there is a strong association between X and Y.

Additional information, often through controlled experiments, is needed to draw cause-and-effect conclusions.

#### 10. General Linear Regression Model
$\beta_k$ indicates the change in mean response with a unit increase in the predictor Xk, when all other predictors are held constant. This change is the same irrespective of all levels at which other predictors are held.

The effect of the predictor variables are addictive add together.
Sometimes the effect of one predictor depends on the values of the other predictors.  Non-additive, interactive 

For example, How education level affects income may depend on gender.
If residual VS the interaction term $X_1X_2$ shows a clear linear pattern. This term should be included in the model. (plotting residuals against various interaction terms)

#### 11. Multicollinearity 

Multicollinearity doesn’t prevent us from getting a good fit of the data.

With Multicollinearity, the estimated regression coefficients tend to have inflated sampling variability (larger standard errors). This leads to:

 (1) Wide confidence intervals

 (2) It’s possible that none of the regression coefficients is statistically significant, but at the same time there is a significant regression relation between the response variable and the entire set of x variables.

###### In the present of multicollinearity:
The regression coefficient of an x variable depends on which other x variables are also in the model.

A regression coefficient does not reflect any inherent effect of the corresponding x variables on the response variable, but only a marginal effect given whatever other x variables are also in the model.

Similarity, the reduction in the total variation in Y ascribed to an x variable must be interpreted as a marginal reduction given other x variables also included in the model.

In practice, VIFk > 10 is often taken as an indicator that multicollinearity is high. The $K_{th}$ diagonal element of the inverse correlation matrix $R_{xx}$ is called the variance inflation factor (VIF) for $\beta_k$.

Forward stepwise procedure often works better than forward selection when there is high multicollinearity.

Multicollinearity remedial measures: Ridge regression 

#### 12. T Test in general linear regression

From the general linear test perspective, each T test is a marginal test, testing whether the marginal effect of an X variable is significant given all other X variables being included in the model.

#### 13. Overfitting/Underfitting

Overfitting: The model fit the observed data very well, but fail to generalize well to new observations.

Underfitting: An underfit model will be less flexible and cannot account for the data.

A model that is underfit will have high training and high testing error while an overfit model will have extremely low training error but a high testing error.

#### 14. Why Model selection ?

Models with many X variables tend to have large sampling variability. They are also hard to maintain and interpret
On the other hand, omission of key X variables leads to biased fitted regression functions and predictions.

The goal of model selection is to choose a subset of X variables which balances between model variance and bias.      
Achieves bias - variance trade-off.
##### Bias - Variance Trade off (model selection)
[Balancing Bias and Variance](https://towardsdatascience.com/balancing-bias-and-variance-to-control-errors-in-machine-learning-16ced95724db)

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515803(1).jpg?raw=true)

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515887(1).jpg?raw=true)

Larger models always have a larger overall variance.
Correct models are unbiased.

For two correct models, the larger model tend to overfit the observed data. On the other hand, the larger models have larger overall variance and thus they have larger overall mean-squared-estimation-error (MSE).

MSE (total error) is an unbiased estimator of the error variance. (MSE = SSE/n-p)

##### variance
Variance refers to the amount by which your estimate of f(X) would change if we estimated it using a different training data set. Since the training data is used to ﬁt the statistical learning method, diﬀerent training data sets will result in a diﬀerent estimation.

Criterion of model selection:
$R^2$
$R_a^2$
Cp  (not far above p, smaller is better)
AIC, BIC (smaller is better)
Press (leave one out cross validation, smaller is better)
press/n and MSPE are the measure of prediction ability of the model (out of sample)    
MSPE based on the validation data is not much larger than SSE/n and press/n based on the training data indicates good predictive ability.
Press not much larger than SSE means there is not severe overfitting by the model.

Criterion of internal validation: SSE, Cp, Press
Criterion of external validation: MSPE VS SSE/n , Press/n

#### 15. Experimental design: Basic Principles 

Replication: deals with uncertainty, allows for generalization.
When a treatment is repeated under the same experimental conditions, any difference observed in the response variable can be attributed to random fluctuation.

If the variation due to random fluctuation is relatively small compared to the total variation in the response variable across treatments, we  would have evidence for treatment effect.

Randomization: deals with confounding factors, allows for causal-effect statements.

Randomization ensures that the comparison between treatments measures the pure treatment effect.

Blocking: reduced known but irrelevant sources of variation, improves efficiency.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515912(1).jpg?raw=true)

#### 16. Confounding variables 

Consider a researcher attempting to assess the effectiveness of drug X, from population data in which drug usage was a patient's choice. The data shows that gender (Z) differences influence a patient's choice of drug as well as their chances of recovery (Y). In this scenario, gender Z confounds the relation between X and Y since Z is a cause of both X and Y:

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515922(1).jpg?raw=true)

For another example, we want to explore the impact of A font / B font to reading speed. There is a confounding variable : the education level of crowd.
In order to get rid of that influence:
1. Randomly sample some people, divide them into two groups according to the level of education (blocking)
2. Randomly assign them to two types of fonts.

#### 17. Selection bias

Often resulting from the method of collecting samples.

#### 18. Right/ left skewed 

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515956(1).jpg?raw=true)

To summarize, generally if the distribution of data is skewed to the left, the mean is less than the median, which is often less than the mode. If the distribution of data is skewed to the right, the mode is often less than the median, which is less than the mean.

#### 19. Z test , T test difference 

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551516293(1).jpg?raw=true)

#### 20. The benefits of a rolling or moving average compared to straight data

Rolling averages are a simple way to get rid of noise (e.g., randomness) out of the time series data. This comes at a price of a time lag in the rolling average reflecting significant trend changes.

#### 21. Difference of AIC and BIC

AIC and BIC are both penalized-likelihood criteria. Both are of the form “measure of fit + complexity penalty”:
AIC = -2*ln(likelihood) + 2*p, and BIC = -2*ln(likelihood) + ln(N)*p,
where p = number of estimated parameters, N = sample size.
Both information criteria are sometimes used for choosing best predictor subsets in regression and often used for comparing nonnested models. When several groups are being compared, the best model is generally the one that minimizes both AIC and BIC. However, AIC is susceptible to overfitting the data, whereas BIC is susceptible to underfitting the data. The reason is that they penalize the free parameters differently, i.e., 2*p in AIC, ln(N)*p in BIC.

AIC always has a chance of choosing too big a model, regardless of n. BIC has very little chance of choosing too big a model if n is sufficient, but it has a larger chance than AIC, for any given n, of choosing too small a model.

#### 22. Standard Deviation vs Standard error

The standard error (SE) of a statistic (usually an estimate of a parameter) is the standard deviation of its sampling distribution or an estimate of that standard deviation. 

#### 23. Overfitting

#### Cross Validation

- Holdout Method
Removing a part of the training data and using it to get predictions from the model trained on rest of the data.
It still suffers from issues of high variance. This is because it is not certain which data points will end up in the validation set and the result might be entirely different for different sets.

- K-Fold Cross Validation
In K Fold cross validation, the data is divided into k subsets. Now the holdout method is repeated k times, such that each time, one of the k subsets is used as the test set/ validation set and the other k-1 subsets are put together to form a training set. The error estimation is averaged over all k trials to get total effectiveness of our model. As can be seen, every data point gets to be in a validation set exactly once, and gets to be in a training set k-1 times. This significantly reduces bias as we are using most of the data for fitting, and also significantly reduces variance as most of the data is also being used in validation set.As a general rule and empirical evidence, K = 5 or 10 is generally preferred.

- Stratified K-Fold Cross Validation
In some cases, a large imbalance in the response variables. 
For example, in dataset concerning price of houses, there might be large number of houses having high price. 
Or in case of classification, there might be several times more negative samples than positive samples. 
For such problems, a slight variation in the K Fold cross validation technique is made, such that each fold contains approximately the same percentage of samples of each target class as the complete set, or in case of prediction problems, the mean response value is approximately equal in all the folds. This variation is also known as Stratified K Fold.

- Leave-P-Out Cross Validation
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


Similarly, for lasso, the equation becomes,$|β_1|+|β_2|≤ S$.
This implies that lasso coefficients have the smallest RSS(loss function) for all points that lie within the diamond given by $|β_1|+|β_2|≤ S$.



![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551741185(1).jpg?raw=true)


The above image shows the constraint functions(green areas), for lasso(left) and ridge regression(right), along with contours for RSS(red ellipse).


Since ridge regression has a circular constraint with no sharp points, this intersection will not generally occur on an axis, and so the ridge regression coeﬃcient estimates will be exclusively non-zero. However, the lasso constraint has corners at each of the axes, and so the ellipse will often intersect the constraint region at an axis. When this occurs, one of the coeﬃcients will equal zero. In higher dimensions(where parameters are much more than 2), many of the coeﬃcient estimates may equal zero simultaneously.


The tuning parameter $\lambda$, used in the regularization techniques described above, controls the impact on bias and variance. As the value of $\lambda$ rises, it reduces the value of coefficients and thus reducing the variance. Till a point, this increase in $\lambda$ is beneficial as it is only reducing the variance(hence avoiding overfitting), without loosing any important properties in the data. But after certain value, the model starts loosing important properties, giving rise to bias in the model and thus underfitting. Therefore, the value of $\lambda$ should be carefully selected.