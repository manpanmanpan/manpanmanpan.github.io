---
layout:     post
title:      AB Testing
subtitle:   
date:       2019-02-28
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - Metric Definition, Filtering and Segmenting, Sensitivity and Robustness, 
---

# AB Testing
## 1. Metric Definition 

### click_through_rate VS click_through Probability


$$\text{click through rate} = \frac{\text{number of clicks}}{\text{number of page views}} (\text{measure the usability})~~ Poisson~ Distribution $$

$$\text{click through probability} = \frac{\text{unique visitors who click}}{\text{unique visitors  to page}} (\text{measure the total impact})~~ Binomial~Distribution $$

### Categories of summary metrics

- Sums and Counts 

  e.g:  # users who visited page

- Means, Medians and Percentiles

  e.g: mean age of users who completed a course or median latency of page load

- Probabilities and Rates

  e.g: Probability has 0 or 1 outcome in each case , Rate has 0 or more

- Ratios

  e.g: $\frac{P(revenue - generating~click)}{P(any~click)}$



## 2. How to filter out sort of (spam or fraud) abuse on you site?

### Filtering and Segmenting

- Filter just the affected traffic to increase the power and sensitivity of your experiment (slice your data, computing your metric on a bunch of disjoint sets).
For example, by country, by language, by platform.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1551747585(1).jpg?raw=true)

week over week plot
We would divide each data point by the corresponding data point from a week ago.

## 3. Sensitivity and Robustness

- Sensitivity: You want to choose a metric that picks up changes you care about.

- Robustness: Robust against changes that you don't care about. So it doesn't move a lot when nothing interesting has happened.

### How to measure the sensitivity and robustness?

- AA Testing

- Retrospective Analysis

For example: 
We want to track the latency of a video, that is how long it takes the video to load. 
There are 5 summary metirc (Median, 80th, 85th, 90th, 99th percentile). How to choose summary metric?

For retrospective analysis, we de-segment the data by different videos (look at the distribution of load time per video).

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/e08ef421f7bb8713b6f1e310897e7bf.png?raw=true)

From the picture above, we get a roughlt similar distribution of load times for the different videos, which indicates they are 5 comparable videos.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/2f9a57632122bffb69c444e0ae07728.png?raw=true)

90th and 99th percentile: not robust enough since they are moving around quite a bit even for videos that are pretty comparable.

For AA testing, it would be great if we had experiments that changed the resolution. It should impact our metric, if it doesn't, the metric isn't sensitive enough. 

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/f115f30996594647d8ac09a4dbe751d.png?raw=true)

Median and 80th percentile: not sensitive enough. They are not showing a change when we do make a change that we care about.

So in this example, 85th percentile is a good choice of a metric that both robust and sensitive.

## 4. Variability

- Analytic Variability ($SE_{pool}$)

- Empirical Variability (Assume normal distribution)

- Nonparametric (order)


## 5.  Choosing a unit of diversion 

##### Changing the unit of diversion will change the empirical estimate of variability

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/2746d79ac705202ef3ceb3690b2986f.png?raw=true)

Three main considerations of choosing a unit of diversion:

- Consistency

- Ethical consideration

- Variability (**unit of analysis [denominator] VS  unit of diversion**)

## 6. Population and Cohort

#### Choosing a cohort also changes your variability

When to use a cohort instead of a population?

- Looking for learning effect (user learning which is related to time)
 
  There are 2 kinds of learning effect: Novelty effect or refuse changing

- Examining user retention

- Want to increase user activity

- Anything requiring user to be established

#### For Example:

To see if changing structure of a exsiting course will improve the completion rate of the entire course.

Unit of diversion: User ID

In this case, we just want to make an experiment for users who start the course after our experiment start time, rather than the whole users who attended to the course.

So the cohort only include users who started the lesson after the experiment was started in the experiment. It is a subset of the population. 

Note: we have to split cohort into an experiment cohort and a control cohort.

## 7. Power, $\alpha$ , $\beta$

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552621279(1).png?raw=true)


## 8. Size and Duration

We need to consider:

When to do experiment (holiday)?

Duration would be related to Fraction of your traffic:
50% cookies run 10 days  VS  25% cookies run 20 days

Split our size to run comparable experiment to detect if there are other reasons would impact our results, for example: holiday/ not holiday, weekends or weekdays (accounting for those other sources of variability). Or run different experiments for different level of the same feature. 

## Calculate the sample size

```
## Strategy: For a bunch of Ns, compute the z_star by achieving desired alpha, then
## compute what beta would be for that N using the acquired z_star. 
## Pick the smallest N at which beta crosses the desired value
# Inputs:
#   The desired alpha for a two-tailed test
#   Returns: The z-critical value

get_z_star = function(alpha) {
  return(-qnorm(alpha / 2))
}
```

```
# Inputs:
#   z-star: The z-critical value
#   s: The standard error of the metric at N=1
#   d_min: The practical significance level
#   N: The sample size of each group of the experiment
# Returns: The beta value of the two-tailed test
get_beta = function(z_star, s, d_min, N) {
  SE = s /  sqrt(N)
  return(pnorm(z_star * SE, mean=d_min, sd=SE))
}
```


```
# Inputs:
#   s: The standard error of the metric with N=1 in each group
#   d_min: The practical significance level
#   Ns: The sample sizes to try
#   alpha: The desired alpha level of the test
#   beta: The desired beta level of the test
#   Returns: The smallest N out of the given Ns that will achieve the desired
#          beta. There should be at least N samples in each group of the experiment.
#          If none of the given Ns will work, returns -1. N is the number of
#          samples in each group.

required_size = function(s, d_min, Ns=1:200000, alpha=0.05, beta=0.2) {
  for (N in Ns) {
    if (get_beta(get_z_star(alpha), s, d_min, N) <= beta) {
      return(N)
    }
  }
  
  return(-1)
}
```


```
# Example analytic usage
# This is the example from Lesson 1, for which the online calculate gave 3,623
# samples in each group

# s is the pooled standard error for N=1 in each group,
# which is sqrt(p*(1-p)*(1/1 + 1/1))
required_size(s=sqrt(0.1*0.9*2), d_min=0.02)
```

```
# Sizing: Example
# Cookie-based diversionrequired_size(s=sqrt(0.1*0.9*2), d_min=0.02)
# Since the standard error is proportional to 1/sqrt(N), s, or
# the standard error for N=1, is equal to the mesaured standard error with 5000
# in each group times sqrt(5000)
required_size(s=0.00515*sqrt(5000), d_min=0.02)
# User-id-based diversion
required_size(s=0.0119*sqrt(5000), d_min=0.02)

# Sizing: Quiz
# Original size
required_size(s=0.0628*sqrt(1000), d_min=0.01, Ns=seq(10, 500000, 100))
# Size with event-based diversion
required_size(s=0.0209*sqrt(1000), d_min=0.01, Ns=seq(10, 500000, 100))
# Size with event-based diversion and English-only traffic
required_size(s=0.0188*sqrt(1000), d_min=0.015)
# Size with cookie-based diversion, English-only traffic, and 
# click-through-probability instead of click-through-rate
required_size(s=0.0445*sqrt(1000), d_min=0.015, Ns=seq(10, 500000, 100))
```


## 9. Sanity Checks before analyzing results

#### 9.1 Choosing invariant metrics (like population sizing metrics)

For example, if we run an experiment to figure out :

if change the order of coursrs in course list will affact which courses users eventually enroll in. **Unit of diversion is user id**. We should make sure # signed in users (should be randomized), # cookies, # events, CTR on "start now" button to courses list page, those are invariant metrics.

Another example:

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552639064(1).png?raw=true)


#### 9.2 Checking Invariants

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552639349.jpg?raw=true)

##### How can we figure out whether the difference of total control and total experiment is within expectation?

Given each cookie is randomly assigned to the control or experiment group with the prob 0.5, just like a fair coin, which is binomial distribution. So we can contruct Binomial confidence interval to figure out whether the difference is within expectation.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552639892(1).jpg?raw=true)

From the CI above, we find our $\hat{p}$ doesn't fall into the CI [0.4973, 0.5027], which means the difference isn't within expectation.

Then, look at the day by day data again.
![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552639948(1).jpg?raw=true)

From above, we find there is no day obviously stands out as the hightest. So we can talk to the engineers to figure out if something was wrong with the experiment setup. Or to try slicing to see if one particular slice is weired, like by country, language or platform to see if one particular slice looks like it's causing the problem. Or checking the age of cookies in each group. Does one group tend to have more new cookies while the other group has older cookies.

## 10. Analyzing the results - Single Metric

The result of a test is below:
![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552776944(1).jpg?raw=true)

### Effect size

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552777428(1).jpg?raw=true)
We can see that the CI does not include zero, these result are statistically significant. It is unlikely that there was no real difference. BUt the CI does include the practical significance boundary 0.01, meaning that I can't be confident at the 95% level that the size of this effect is something that I care about.

### Sign Test

To do the sign test, we need to look at the day by day data again, and count the number of days where the CTR is higher in experiment group.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552777947(1).jpg?raw=true)

$$ two ~tail~ P~value =2* P(y \ge 9) = 0.4240$$

So the sign test has no statistically significant.

Sign test has lower power than effect size test, which is frequently the case for nonparametric tests. That's the price you pay for not making any assumptions.

Need digging deeper: Weekends / Weekdays

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552778899(1).jpg?raw=true)

We find all four weekend days are positive, which much higher than the CTR on other positive change days. This suggests that the change may be has a small effect or no effect during the week, but a larger effect on weekends. Then, we can calculate the effect size and sign test for weekdays and weekends separately.

**Recommendation**: Not launching the experiment at this point. Instead dig deeper into why the change didn't affect weekday visitors.

## 11. Gotchas: Simpson’s Paradox

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552779468(1).jpg?raw=true)

## 12. Analyzing Multiple Metrics

Find an overall evaluation criteria

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552783515(1).jpg?raw=true)

The Bonferroni method is likely to be too consercative, we recommend to use a more sophisticated method than Bonferoni, ideally one that takes into account the fact that the metrics are likely to be correlated.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552806795(1).jpg?raw=true)

In the above example, cause we have at least one false positive every time. So the FWER or the overall $\alpha = 1$, while FDR is 0.05, since most of the metrics that you are claiming have a significant difference actually do.

If you are trying to detect significant changes arcoss a large number of metrics, FDR can be more lenient.

## 13. Gotchas: Changes Over Time

For Example: **Seasonality effects**

Students, summer vacation causes internet changes; Holidays, Black friday causes shopping behavior will be changed.

Capture these seasonal or event-driven impacts: Holdback. The idea is that you lanuch your change to everyone expect for a small holdback. A set of users, that don't get the change, so you can continue comparing their behavior to the control.

Another example: **Novelty effect / change aversion**. Then, Cohort analysis can be helpful.

Also, **budgets**. If you don't control for the budgets properly, the effect can change as you ramp up.



##  Summary

Nowadays it’s very common for companies to do A/B tests on web page versions, personalized recommendations and new features.

