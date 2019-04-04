---
layout:     post
title:      Interview Questions
subtitle:   
date:       2019-04-03
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - DS, BA
---


## 1. Outlier detection VS Novelty detection

Novelty detection: the identification of new or unknown data that a machine learning system has not been trained with and was not previously aware of, with the help of either statistical or machine learning based approaches. (i.e. during the model training, all the data are clean data)

Outlier detection: the identification of items, events or observations which do not conform to an expected pattern or other items in a dataset. (i.e. in the case of outlier detection, the dataset has already been polluted.) 

Outlier detection is similar to novelty detection in the sense that the goal is to separate a core of regular observations from some polluting ones, called “outliers”. Yet, in the case of outlier detection, we don’t have a clean data set representing the population of regular observations that can be used to train any tool.


**Methods to do the outlier detection:**

To univariate data:
Check the frequency distribution of the data
Box-plot: An outlier is a point of data that lies over 1.5 IQRs below the first quartile (Q1) or above third quartile (Q3) in a given data set.

To multivariate data:
Proximity based methods:1) Cluster based methods 2)Distance based methods 3) Density based methods
Such as One-class SVM, Isolation Forest, …

Reference:
[Novelty and Outlier Detection](https://scikit-learn.org/stable/modules/outlier_detection.html)

[Introduction to Outlier Detection Methods](https://www.datasciencecentral.com/profiles/blogs/introduction-to-outlier-detection-methods)

