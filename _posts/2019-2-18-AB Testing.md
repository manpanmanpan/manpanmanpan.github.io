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


$$\text{click through rate} = \frac{\text{number of clicks}}{\text{number of page views}} (\text{measure the usability}) $$

$$\text{click through probability} = \frac{\text{unique visitors who click}}{\text{unique visitors  to page}} (\text{measure the total impact}) $$

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

- Analytic Variability

- Empirical Variability (Assume normal distribution)

- Nonparametric 


## 5.  Choosing a unit of diversion

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/2746d79ac705202ef3ceb3690b2986f.png?raw=true)

Three main considerations of choosing a unit of diversion:

- Consistency

- Ethical consideration

- Variability (unit of analysis [denominator] VS  unit of diversion)

