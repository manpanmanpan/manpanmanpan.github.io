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
#### Event: the time at which the customer would be charged-off.
#### Time of origin: Accounts open date
#### Time scale: Years / Months

The difference between the time of event and the time origin gives us the time to event.

### 2. Mathematical Intuition

Lets assume a **non-negative continuous random variable T**, representing the time until accounts charged off.

- T is the time from customer’s(a randomly selected customer) subscription to the customer charged-off.

F(t) = P (T< t) ; here , F(t) gives us the probability that the event has occurred by duration t. F(t) gives us the proportion of population with the time to event value less than t.      $ \int_{0}^t f(x)dx$

**Survival Function:** S(t) = 1 - F(t)= P(T ≥t); S(t) gives us the probability that the event has not occurred by the time t . In simple words, S(t) gives us the proportion of population with the time to event value more than t.