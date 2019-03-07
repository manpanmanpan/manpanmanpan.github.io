---
layout:     post
title:      Logistic Regression
subtitle:   
date:       2019-03-06
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - Logistic Regression, Gradient Descent
---

### Logistic Regression

### Binary logistic regression

### 1. Sigmoid activation

$$ S(z) = \frac{1}{1+e^{-z}} $$

Let $Z= X^T\beta$, then we have:

$$ P(Y=1|X) = \frac{1}{1+e^{-X^T\beta}} = \frac{e^{X^T\beta}}{1+e^{X^T\beta}} $$

$$ P(Y=0|X) = 1-P(Y=1|X)= \frac{1}{1+e^{X^T\beta}} $$

We can rewrite it as (0,1 coding): 
$$P(Y|X) = \frac{e^{Y*X^T\beta}}{1+e^{X^T\beta}} $$

$$ logit(P(Y=1|X)) = log\frac{P(Y=1|X)}{1-P(Y=1|X)} = X^T\beta$$

### 2. Cost Function

Y ~ Bernoulli (y, p)

$P(Y=y\mid X) = p^y(1-p)^{1-y}$
where $p = P(Y=1\mid X) = \frac{1}{1+e^{-x^T\beta}} = \frac{e^{x^T\beta}}{1+e^{x^T\beta}}$


We can use maximum likelihood method to estimate $\beta$.

$L(\beta) = \sum_{i=1}^n log~p_i^{y_i}(1-p_i)^{1-y_i}$
$= \sum_{i=1}^n [y_i~log(\frac{e^{x_i^T\beta}}{1+e^{x_i^T\beta}}) +(1-y_i)~log(\frac{1}{1+e^{x_i^T\beta}})] $
$= \sum_{i=1}^n[y_ix_i^T\beta-log(1+e^{x_i^T\beta})] $

Then, we need to maximize the $L(\beta)$ by minimizing loss function:

$$ \sum_{i=1}^nl(x_i, y_i, \beta) = \sum_{i=1}^n-y_ix_i^T\beta + log(1+e^{x_i^T\beta}) $$

### 3. Gradient Descent

For $x_i, y_i$

$$l(y_i,x_i,\beta) = -y_ix_i^T\beta + log(1+e^{x_i^T\beta}) $$

$$y_i~~(1*1),~x_i~~(p*1),~\beta~~(p*1)$$

$$ \frac{\partial l}{\partial \beta} = -y_ix_i + \frac{e^{x_i^T\beta}x_i}{1+e^{x_i^T\beta}} = x_i(p_i-y_i)$$

Then 

$$\beta^{t+1} = \beta^t - \alpha * gradient $$

##### Vectorized:

$$R_n(\beta) = \frac{1}{n}\sum_{i=1}^nl_i$$

$$ Gradient: \frac{\partial R_n(\beta)}{\partial \beta} = \frac{1}{n}\sum_{i=1}^nx_i(p_i-y_i) == \frac{1}{n}X^T\gamma $$

$$X~~n*p, \gamma~~n*1, \gamma_i = p_i - y_i $$

### 4. Newton-Raphson Method

##### Background of Newton Method:

From Taylor Expansion:

$$ f(x) = f(x_0) + f'(x_o)(x - x_0) + \frac{(x-x_0)^2}{2}f''(x_1) ~~~~ x1\in(x,x_0)$$

If we want $f(x) = 0$ , then

$$ 0 = f(x)\approx f(x_0) + f'(x_0)(x - x_0) ~~~~ x\approx x_0 $$

So

$$ x \approx x_0 - \frac{f(x_0)}{f'(x_0)} $$

When we want to min our cost function, we have to let $f'(x) = 0$, then it comes:

$$ x^{t+1} = x^t - \frac{f'(x^t)}{f''(x^t)} $$


For $x_i, y_i$

$ \frac{\partial^2 l_i}{\partial \beta \partial \beta^T} = \frac{\partial (-y_ix_i + \frac{x_ie^{x_i^T\beta}}{1+e^{x_i^T\beta}}) }{\partial \beta^T} = \frac{(x_i\frac{\partial e^{x_i^T\beta}}{\partial \beta^T})(1+e^{x_i^T\beta})- x_ie^{x_i^T\beta}\frac{\partial (1+e^{x_i^T\beta})}{\partial \beta^T}   }{(1+e^{x_i^T\beta})^2} = \frac{x_ix_i^Te^{x_i^T\beta}(1+e^{x_i^T\beta})-x_ix_i^Te^{2x_i^T\beta}}{(1+e^{x_i^T\beta})^2} = \frac{x_ix_i^Te^{x_i^T\beta}}{(1+e^{x_i^T\beta})^2} = x_ix_i^Tp_i(1-p_i)$

##### Vectorized:

$$ Hessian: \frac{\partial^2 R_n(\beta)}{\partial \beta \partial \beta^T} = \frac{1}{n}\sum_{i=1}^n x_ix_i^Tp_i(1-p_i)== \frac{1}{n}X^TwX$$

where $w$ is a Diagonal matrix, Diagonal element is $p_i(1-p_i)$.

$$X~~n*p, w ~~ n*n $$


$$ Gradient: \frac{\partial R_n(\beta)}{\partial \beta} = \frac{1}{n}\sum_{i=1}^nx_i(p_i-y_i) == \frac{1}{n}X^T\gamma $$

$$X~~n*p, \gamma~~n*1, \gamma_i = p_i - y_i $$

Then

$$\beta^{t+1} = \beta^t - (\frac{\partial^2 R_n(\beta)}{\partial \beta \partial \beta^T})^{-1}\frac{\partial R_n(\beta)}{\partial \beta} $$



