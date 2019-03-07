---
layout:     post
title:      Probability and Statistics
subtitle:   P value, Power, CI
date:       2019-02-28
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - P value, Power, CI
---
#### 1. What is P-value?

Assume that you observe a sample value, e.g. $\bar{x}$ = x, p value = probability under H<sub>0</sub> that you observe a sample as **extreme** as or more extreme than x.
    what constitutes "extreme" depends on the alternative hypothesus.
For instance p value = P( $\bar{x}$ >= x) if $H_1 = \mu > \mu_0$


P-value is the probability of obtaining a result at least as extreme as the current one, assuming that the null hypothesis is true.

For example:
Imagine we did a study comparing a placebo group to a group that received a new blood pressure medication and the mean blood pressure in the treatment group was 20 mm Hg lower than the placebo group. Assuming the null hypothesis is correct the pvalue is the probability that if we repeated the study the observed difference between the group averages would be at least 20.

#### 2.  Power, Type 1 error, Type 2 error, $\alpha$

Type 1 Error = incorrectly rejecting the null hypothesis. (Probability of false alarm)

Type 2 Error = fail to reject null when you should have rejected the null hypothesis.(Probability of missed detection)

Power is the probability of finding a difference between groups if one truely exists. It is the percentage chance that you will be able to reject the null hypothesis if it is really false.

Power Function: the power function of a test with rejection region $R$ is the function of $\theta \in \Theta_1$ defined as $ \beta(\theta) = P_{\theta}(X\in R)$.

Ideally,

$$ \beta(\theta) = 0, if~ \theta \in \Theta_0$$

$$\beta(\theta) = 1, if~ \theta \in \Theta_1$$

Usually, it's hard to achieve, so we always minimize the type Ⅱ error after controlling the type I error.

Notice,

$$ \theta\in\Theta_0 ~~~~ \beta(\theta) = prob~of~type~I~error$$

$$ \theta\in\Theta_1 ~~~~ 1- \beta(\theta) = prob~of~type~Ⅱ~error$$

$\alpha$ (size of a test): A test with power function $\beta(\theta)$ is a size $\alpha$ test if $sup_{θ∈Θ_0}β(θ)\leα$.


#### 3. Confidence Interval 

To construct CI, we have to find the pivot.
Pivot, a random variable $Q(X,θ)$ of $X$ and $θ$ is called a pivot if the distribution of $Q$ does not involve $\theta$.

Pivot:

$X_1, X_2..... X_n \sim N(\mu, \sigma^2) $

(1) C.I for $\mu, \sigma^2$ known,  $\frac{\bar{x} - \mu}{\sigma/\sqrt{n}} \sim N(0,1)$

(2) C.I for $\mu, \sigma^2$ unknown, $\frac{\bar{x} - \mu}{S/\sqrt{n}} \sim t_{n-1}$

(3) C.I for $\sigma^2$, $\mu$ known,  $\sum_{i=1}^n(\frac{x_i - \mu}{\sigma})^2 \sim \chi^2_n$

(4) C.I for $\sigma^2$, $\mu$ unknown,  $\sum_{i=1}^n(\frac{x_i - \bar{x}}{\sigma})^2 \sim \chi^2_{n-1}$



Confidence interval provides a range of values which is likely to contain the population parameter of interest, we would like to think the parameter is a fixed value usually.

Interpretation : We have 95% confident that the true value is between [L,R]

#### 4. Z test , T test difference 

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551516293(1).jpg?raw=true)

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551936871(1).png?raw=true)