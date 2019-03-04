---
layout:     post
title:      Business Questions
subtitle:   Business
date:       2019-03-02
author:     Cassie Pan
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Business
---

### Q1: You are a DS and you track the metric “# of job views” each week. Last week the metric went down by 20%, how will you investigate this drop?

When we come to the question, we should have a clear definition of the metric '# of job views', then consider how to get to the metric from the user's perspective. 

Considering that you are a job seeker, you should do job search, then you get some results in some order after your quarry, then you click some jobs you are interested in. Finally, we will get the number of job views. 

For each step, when we track the metric # of job views drop, we can track:

##### Whether # of job search drops or not?
##### Search results are better or not? rank? Is there any problem for ranking algorithm? or results' job title/subtitle has some change?
##### How about the number of job opening during that period?
##### Whether that time is the period of graduation season (# of job views drop is a normal phenomenon)?
- compare # of job views during the same period in last year


#### Seasonality Analysis
- year to year
- quarter to quarter (graduation period)
- monthly to monthly
- week to week (more job views during the weekend, Monday would drop)

#### Break down Analysis (different dimension)
- Country
- Device (desktop job views/ mobie app job views(Android or iphone))
- new user or old user

#### Tracking issue