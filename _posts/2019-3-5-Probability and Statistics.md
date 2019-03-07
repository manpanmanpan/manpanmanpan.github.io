---
layout:     post
title:      Probability and Statistics
subtitle:   P value, Power, CI, Hypothesis Testing
date:       2019-3-06
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - P value, Power, CI, Hypothesis Testing
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

###### Why do we reject $H_0$ when P value $< ~ \alpha $ ?




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

#### 5. Hypothesis Testing

[Hypothesis Testing for Means & Proportions](http://sphweb.bumc.bu.edu/otlt/MPH-Modules/BS/BS704_HypothesisTest-Means-Proportions/BS704_HypothesisTest-Means-Proportions_print.html)

#### 5.1 Likelihood Ratio Test

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551948361(1).jpg?raw=true)

##### Q. How will you test if a coin is fair or not?

$$ H_0 : p = \frac{1}{2} ~~~~~~ H_1: p \neq \frac{1}{2}$$

$$ x \sim Bernoulli(p)$$

$$ P(x=x_i) = p^{x_i}(1-p)^{1-{x_i}} $$

$$ L = \prod_{i=0}^np^{\sum_{}{x_i}}(1-p)^{n-\sum_{}{x_i}} = p^y(1-p)^{n-y} ~~~where~y~is~the~number~of~heads$$

Then, we calculate $\lambda(x)$, the $MLE$ of p under $\Theta$ is $\hat{p} = \frac{y}{n}$, so

$$ \lambda(x)= \frac{sup_{\theta\in\Theta_0}L(\theta\mid x)}{sup_{\theta\in\Theta}L(\theta\mid x)} = \frac{p_0^y(1-p_0)^{n-y}}{\hat{p}^y(1-\hat{p})^{n-y}} = \frac{\frac{1}{2}^n\frac{1}{2}^{n-y}}{\frac{y}{n}^n(1-\frac{y}{n})^{n-y}} = 2^{-n}n^ny^{-y}(n-y)^{y-n}   $$

We know $LRT$ rejection region is $\lambda(x) < c $

$$ \frac{\partial log(\lambda(x))}{\partial y} = log(n-y)-log(y) = 0 $$

$$ y = \frac{n}{2} $$

$\lambda(x)$ is increasing if $y<\frac{n}{2}$, $\lambda(x)$ is decreasing if $y>\frac{n}{2}$.

So, rejection region $\lambda(x) < c $ is equivalent to $ y >c_1~or~y < c_2$.

The values of $c_1$ and $c_2$ depend on the level of significance. For example, we throw coins 6 times, we would reject null hypothesis if $\sum_{}{x_i} \ge 5~or~\sum_{}{x_i} \le 1$, then we can calculate the type I error.

$$ \alpha (type~I~error) = P(\sum_{}{x_i} \ge 5~or~\sum_{}{x_i} \le 1 \mid H_0) = C_6^5(\frac{1}{2})^6 + C_6^6(\frac{1}{2})^6 + C_6^1(\frac{1}{2})^6 + C_6^0(\frac{1}{2})^6 = \frac{7}{32} = 0.21875$$

Then, we get our sample value, calculate P value. If the p value < $\alpha$, we reject $H_0$, if the P value > $\alpha$, we fail to reject $H_0$.

**Notice**: Maximizing a likelihood function is equivalent to maximizing its natural logarithm. Because the natural logarithm log is a continuous convex function that is strictly increasing in the range of the likelihood function.

#### 5.2 Asymptotic distribution of the LRT—simple H0

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551995331(1).jpg?raw=true)

##### Q. How will you test if a dice is fair or not?

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551997096.jpg?raw=true)



By the way, we use the **Lagrange Multiplier** to get $\hat{p_j}$:

$$ log(L) = y_1log(p_1) + y_2log(p_2) + y_3log(p_3) + y_4log(p_4) + y_5log(p_5) + y_6log(p_6) $$

We want $max~log(L)$ subject to $ P_1 + P_2 +P_3+P_4+P_5+P_6-1 =0$.

Define:

$$ F = log(L) - \lambda(P_1 + P_2 +P_3+P_4+P_5+P_6-1) $$

By solving:

$$\left( \begin{array}{c}
    \frac{\partial F}{\partial P_1}  \\
    \frac{\partial F}{\partial P_2}  \\
    ......\\
    \frac{\partial F}{\partial \lambda}
\end{array}\right)=
\left( \begin{array}{c}
    0  \\
    0  \\
    ......\\
    0
\end{array}\right)
$$

Finnally, we get $$\hat{P_i} = \frac{y_i}{n}$$.
