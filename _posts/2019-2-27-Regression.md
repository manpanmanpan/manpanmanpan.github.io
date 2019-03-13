---
layout:     post
title:      Regression
subtitle:   Regression
date:       2019-02-27
author:     Cassie Pan
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Regression, AIC / BIC, Overfitting, Underfitting, Bias and Variance trade off, Multicollinearity, Right / Left skewed, Confounding variables
---

#### 1. Least Square Principle 

Least square principle is to fit the observed data by minimizing the sum of squared vertical deviations.

#### 2. Residuals
![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551495156(1).jpg?raw=true)

#### 3. SSTO &  SSR &  SSE
SSTO = SSR + SSE

Total deviations  (the variation of the observed Yi around their sample mean) can be decomposed into the sum of two items: 
The deviation of observed value around the fitted regression line (residual) and the deviation of fitted value from the mean.

SSR = SSTO - SSE

Is the effect of X in reducing the variation in Y through linear regression. 

SSR is the reduction in uncertainty in predicting Y by utilizing the predictor X through a linear regression model.

#### 4. $R^2$ ,  $R_a^2$
$R^2$ = SSR/SSTO = 1 - SSE/SSTO

$R^2$ is the proportional reduction of the total variation in Y by explaining Y using X through a linear regression model.

For example: $R^2$ = .209 ( y child’s height, x parents’ height )
20% of variation in child’s height may be explained by the variation in parents’ height.

Sometimes, nonlinearity pattern shows larger $R^2$ .
Adding more X variables to the model will always increase $R^2$.

$R_a^2$ = 1 - MSE/MSTO = 1 - n-1/n-p * SSE/SSTO  <= $R^2$

$R_a^2$ may become decrease when adding more X variables into the model because the decrease in SSE may be more than offset by the loose of degrees of freedom in SSE.

#### 5. Model diagnostics
##### Assumptions of the simple linear model with normal errors:
######  (1). Linearity of the regression relation  (residual vs predictor variables plot)

###### (2). Normality of the error terms  (QQ plot)

###### (3). Constant variance of error terms
 ( if the residual vs predictor variable plot (or residual vs fitted value plot) shows unequal dispersion along the horizontal xi_s, then this is an indicator of unequal variance)

TESTS OF EQUAL VARIANCE ( Hartley Test, Brown-Forsythe Test, Bartlett Test)

Unequal error variance remedial measures: Transformation of observation variable Y, ex, BOX-COX procedure; Weighted least squares.

###### (4). Independence of the error terms  
(if measurements are obtained in a time/space sequence, a residual sequence plot can be used to check whether the error terms are serially correlated)

#### 6. Regression and Causation 
Regression analysis by itself doesn’t imply cause and effect relation
A strong regression relation neither implies ‘X causes Y’ nor implies ‘Y causes X’. It only means that there is a strong association between X and Y.

Additional information, often through controlled experiments, is needed to draw cause-and-effect conclusions.

#### 7. General Linear Regression Model
$\beta_k$ indicates the change in mean response with a unit increase in the predictor Xk, when all other predictors are held constant. This change is the same irrespective of all levels at which other predictors are held.

The effect of the predictor variables are addictive add together.
Sometimes the effect of one predictor depends on the values of the other predictors.  Non-additive, interactive 

For example, How education level affects income may depend on gender.
If residual VS the interaction term $X_1X_2$ shows a clear linear pattern. This term should be included in the model. (plotting residuals against various interaction terms)

#### 8. Multicollinearity 

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

#### 9. T Test in general linear regression

From the general linear test perspective, each T test is a marginal test, testing whether the marginal effect of an X variable is significant given all other X variables being included in the model.

#### 10. Overfitting/Underfitting

Overfitting: The model fit the observed data very well, but fail to generalize well to new observations.

Underfitting: An underfit model will be less flexible and cannot account for the data.

A model that is underfit will have high training and high testing error while an overfit model will have extremely low training error but a high testing error.

#### 11. Why Model selection ?

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

$C_p$  (not far above p, smaller is better)

AIC, BIC (smaller is better)

Press (leave one out cross validation, smaller is better)

press/n and MSPE are the measure of prediction ability of the model (out of sample)    

MSPE based on the validation data is not much larger than SSE/n and press/n based on the training data indicates good predictive ability.

Press not much larger than SSE means there is not severe overfitting by the model.

Criterion of internal validation: SSE, Cp, Press

Criterion of external validation: MSPE VS SSE/n , Press/n

#### 12. Experimental design: Basic Principles 

Replication: deals with uncertainty, allows for generalization.
When a treatment is repeated under the same experimental conditions, any difference observed in the response variable can be attributed to random fluctuation.

If the variation due to random fluctuation is relatively small compared to the total variation in the response variable across treatments, we  would have evidence for treatment effect.

Randomization: deals with confounding factors, allows for causal-effect statements.

Randomization ensures that the comparison between treatments measures the pure treatment effect.

Blocking: reduced known but irrelevant sources of variation, improves efficiency.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515912(1).jpg?raw=true)

#### 13. Confounding variables 

Consider a researcher attempting to assess the effectiveness of drug X, from population data in which drug usage was a patient's choice. The data shows that gender (Z) differences influence a patient's choice of drug as well as their chances of recovery (Y). In this scenario, gender Z confounds the relation between X and Y since Z is a cause of both X and Y:

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515922(1).jpg?raw=true)

For another example, we want to explore the impact of A font / B font to reading speed. There is a confounding variable : the education level of crowd.
In order to get rid of that influence (Blocking):
1. Randomly sample some people, divide them into two groups according to the level of education (blocking)
2. Randomly assign them to two types of fonts.

#### 14. Selection bias

Often resulting from the method of collecting samples.

#### 15. Right/ left skewed 

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515956(1).jpg?raw=true)

To summarize, generally if the distribution of data is skewed to the left, the mean is less than the median, which is often less than the mode. If the distribution of data is skewed to the right, the mode is often less than the median, which is less than the mean.

#### 16. The benefits of a rolling or moving average compared to straight data

Rolling averages are a simple way to get rid of noise (e.g., randomness) out of the time series data. This comes at a price of a time lag in the rolling average reflecting significant trend changes.

#### 17. Difference of AIC and BIC

AIC and BIC are both penalized-likelihood criteria. Both are of the form “measure of fit + complexity penalty”:

$$AIC = -2*ln(likelihood) + 2*p$$

$$BIC = -2*ln(likelihood) + ln(N)*p$$

where p = number of estimated parameters, N = sample size.
Both information criteria are sometimes used for choosing best predictor subsets in regression and often used for comparing nonnested models. When several groups are being compared, the best model is generally the one that minimizes both AIC and BIC. However, AIC is susceptible to overfitting the data, whereas BIC is susceptible to underfitting the data. The reason is that they penalize the free parameters differently, i.e., 2*p in AIC, ln(N)*p in BIC.

AIC always has a chance of choosing too big a model, regardless of n. BIC has very little chance of choosing too big a model if n is sufficient, but it has a larger chance than AIC, for any given n, of choosing too small a model.

#### 18. Standard Deviation vs Standard error

The standard error (SE) of a statistic (usually an estimate of a parameter) is the standard deviation of its sampling distribution or an estimate of that standard deviation. 