---
layout:     post
title:      Survival Analysis
subtitle:   Time to event analysis - Kohl's Customer
date:       2019-07-20
author:     Cassie Pan
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Survival 
---


### 1. Definition: 
- Event: the time at which the customer would be charged-off.
- Time of origin: Accounts open date
- Time scale: Years / Months

The difference between the time of event and the time origin gives us the time to event.

### 2. Mathematical Intuition

Lets assume a **non-negative continuous random variable T**, representing the time until accounts charged off.

- T is the time from customer’s(a randomly selected customer) subscription to the customer charged-off.

#### 2.1   **Cdf:**
 F(t) = P (T< t) ; here , F(t) gives us the probability that the event has occurred by duration t. F(t) gives us the proportion of population with the time to event value less than t.      $ \int_{0}^t f(x)dx$

#### 2.2  **Survival Function S(t):** 
S(t) = 1 - F(t)= P(T ≥t); S(t) gives us the probability that the event has not occurred by the time t . In simple words, S(t) gives us the proportion of population with the time to event value more than t.  $ \int_{t}^{\infty} f(x)dx$

#### 2.3  **Hazard Function h(t):**

The rate at which event is taking place, out of the surviving population at any given time t. In medical terms, we can define it as “out of the people who survived at time t, what is the rate of dying of those people”.

$$ h(t) = [( S(t) -S(t + dt) )/dt] / S(t) \   limit \ dt → 0 $$



Note: 
- Number of people surviving at t is S(t)*P and the number of people surviving at t+dt is S(t+dt)*P. Number of people died during dt is (S(t) -S(t + dt))*P. Instantaneous rate of people dying at time t is (S(t) -S(t + dt))*P/dt.

- Proportion Surviving at time t: S(t); We also know the surviving population at time t, S(t)*P.

- Thus dividing number of people died in time dt, by the number of people survived at any time t, gives us the hazard function **as measure of RISK of the people dying, which survived at the time t**.


The hazard function is not a density or a probability. However, we can think of it as the probability of failure in an inﬁnitesimally small time period between (t) and (t+ dt) given that the subject has survived up till time t. In this sense, the hazard is a measure of risk: the greater the hazard between times t1 and t2, the greater the risk of failure in this time interval.


#### 2.4  **h(t) = f(t)/S(t)** 
Since that ( S(t) -S(t + dt) )/dt = f(t)


### 3. Kaplan-Meier Estimate

Non-parametric method to estimate the survival curve.

$$ {\hat{S(t)}} = \prod_{i: \ t_i \ \le \ t} \frac{n_i - d_i}{n_i} $$

- $n_i$ is deﬁned as the population at risk at time just prior to time $t_i$; 
- $d_i$ is defined as number of events occurred at time $t_i$

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/Capture.PNG?raw=true)


### 4. Cox Proportional Hazard Model

In this case, we are often interested in how covariates (features[customer’s gender, monthlyincome, days past due, balance etc.])impacts the survival probability function.

In such cases, it is the conditional survival function $ S(t|x) = P(T > t|x)$. Here x denotes the covariates / features. 

**Harzard function:** 

$$ h(t|X = x) = h_0(t) exp(x^T\beta)$$

- β is the vector of coeﬃcients of each covariate. 
- The function $h_o(t)$ is called the baseline hazard function.
- The Cox model assumes that the covariates have a linear multiplication eﬀect on the hazard function and the eﬀect stays the same across time.

The idea behind the model is that the log-hazard of an individual is a linear function of their static covariates, and a population-level baseline hazard that changes over time. 

$$  H(t|x) = exp(x^T\beta)\int_{0}^t h_0(s)ds = exp(x^T\beta) H_0(t) $$


Creating the survival curves at each customer level helps us in proactively creating a tailor made strategy for high-valued customers for different survival risk segments along the timeline.