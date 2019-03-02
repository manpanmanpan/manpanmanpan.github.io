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

[link]()

#### 1. What is P-value?

Assume that you observe a sample value, e.g. $\bar{x}$ = x, p value = probability under H<sub>0</sub> that you observe a sample as extreme as or more extreme than x.
    what constitutes "extreme" depends on the alternative hypothesus.
For instance p value = P( $\bar{x}$ >= x) if H<sub>1</sub> = u > u<sub>0


P-value is the probability of obtaining a result at least as extreme as the current one, assuming that the null hypothesis is true.

For example:

Imagine we did a study comparing a placebo group to a group that received a new blood pressure medication and the mean blood pressure in the treatment group was 20 mm Hg lower than the placebo group. Assuming the null hypothesis is correct the p-value is the probability that if we repeated the study the observed difference between the group averages would be at least 20.

#### 2.  

Type 1 Error = incorrectly rejecting the null hypothesis.
Type 2 Error = fail to reject null when you should have rejected the null hypothesis.

Power is the probability of finding a difference between groups if one truly exists. It is the percentage chance that you will be able to reject the null hypothesis if it is really false.

#### 3.

Least square principle is to fit the observed data by minimizing the sum of squared vertical deviations.

#### 4.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551495156(1).jpg?raw=true)

#### 5. 
SSTO = SSR + SSE

Total deviations  (the variation of the observed Yi around their sample mean) can be decomposed into the sum of two items: 
The deviation of observed value around the fitted regression line (residual) and the deviation of fitted value from the mean.

SSR = SSTO - SSE

Is the effect of X in reducing the variation in Y through linear regression. 

SSR is the reduction in uncertainty in predicting Y by utilizing the predictor X through a linear regression model.

#### 6.
R2 = SSR/SSTO = 1 - SSE/SSTO

R2 is the proportional reduction of the total variation in Y by explaining Y using X through a linear regression model.

For example: R2 = .209 ( y child’s height, x parents’ height )
20% of variation in child’s height may be explained by the variation in parents’ height.

Sometimes, nonlinearity pattern shows larger R2 .
Adding more X variables to the model will always increase R2.

Ra2 = 1 - MSE/MSTO = 1 - n-1/n-p * SSE/SSTO  <= R2

Ra2 may become decrease when adding more X variables into the model because the decrease in SSE may be more than offset by the loose of degrees of freedom in SSE.

#### 7. Confidence Interval Interpretation
Confidence interval provides a range of values which is likely to contain the population parameter of interest.

We have 95% confident that the true value is between [L,R]

#### 8. Model diagnostics
Assumptions of the simple linear model with normal errors:
Linearity of the regression relation  (residual vs predictor variables plot)

Normality of the error terms  (QQ plot)

Constant variance of error terms
 ( if the residual vs predictor variable plot (or residual vs fitted value plot) shows unequal dispersion along the horizontal xi_s, then this is an indicator of unequal variance)

TESTS OF EQUAL VARIANCE ( Hartley Test, Brown-Forsythe Test, Bartlett Test)

Unequal error variance remedial measures: Transformation of observation variable Y, ex, BOX-COX procedure; Weighted least squares.

Independence of the error terms  

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

 Wide confidence intervals

It’s possible that none of the regression coefficients is statistically significant, but at the same time there is a significant regression relation between the response variable and the entire set of x variables.

In the present of multicollinearity:

The regression coefficient of an x variable depends on which other x variables are also in the model.

A regression coefficient does not reflect any inherent effect of the corresponding x variables on the response variable, but only a marginal effect given whatever other x variables are also in the model.

Similarity, the reduction in the total variation in Y ascribed to an x variable must be interpreted as a marginal reduction given other x variables also included in the model.

In practice, VIFk > 10 is often taken as an indicator that multicollinearity is high. The $K_{th}$ diagonal element of the inverse correlation matrix $R_{xx}$ is called the variance inflation factor (VIF) for $\beta_k$.

Forward stepwise procedure often works better than forward selection when there is high multicollinearity.

Multicollinearity remedial measures: Ridge regression 

#### 12. 

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
![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515803(1).jpg?raw=true)

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515887(1).jpg?raw=true)

Larger models always have a larger overall variance.

Correct models are unbiased.

For two correct models, the larger model tend to overfit the observed data. On the other hand, the larger models have larger overall variance and thus they have larger overall mean-squared-estimation-error (MSE).

Under-fit models tend to underfit the observed data.

MSE (total error) is an unbiased estimator of the error variance. (MSE = SSE/n-p)

Criterion of model selection:
R2
Ra2
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

研究扁平化字体和衬线体字体对阅读速度的影响。这里有个混杂变量（confounding variable）就是人群的文化程度。为了消除它的影响，1 随机取样一些人，把他们按照文化水平分两拨，2 随机分配到两种字体。

#### 17. Selection bias

Often resulting from the method of collecting samples.

#### 18. Right/ left skewed 

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551515956(1).jpg?raw=true)

To summarize, generally if the distribution of data is skewed to the left, the mean is less than the median, which is often less than the mode. If the distribution of data is skewed to the right, the mode is often less than the median, which is less than the mean.

#### 19. Z test , T test difference 

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551516293(1).jpg?raw=true)

#### 20. The benefits of a rolling or moving average compared to straight data

Rolling averages are a simple way to get rid of noise (e.g., randomness) out of the time series data. This comes at a price of a time lag in the rolling average reflecting significant trend changes.

