---
layout:     post
title:      Little Book 
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
[Novelty and Outlier Detection](https://scikit-learn.org/stable/modules/outlier_detection.html) !!!

[Introduction to Outlier Detection Methods](https://www.datasciencecentral.com/profiles/blogs/introduction-to-outlier-detection-methods)

## 2. missing values

- Should we even treat missing values is another important point to consider? If 80% of the values for a variable are missing then you may drop the variable instead of treating the missing values.
- Deleting the observations: when your have sufficient data points and your delete will not introduce bias
- Imputation with mean / median / mode or set default value
- Imputation with some models: KNN, Mice etc.
- Use other features to build a model to predict the missing part


## 3. PCA

Suppose we want to analyze a dataset with n observations on a set of p features. When p is very large, it is likely that none of the features alone will be informative since each just contain a very small fraction of the total information.  
Each of the n observations lives in p-dimensional space, but these p dimensions are not equally interesting.  
PCA seeks to **find a small number of dimensions** that are as interesting as possible, where the concept of ‘interesting’ is measured by the amount that the observations vary along each dimension.

Each of the dimensions found by PCA is a linear combination of the p features. For instance, the first principal component is:
$$ Z_{i1} = \phi_{11}x_{i1} + \phi_{21}x_{i2} + .... +\phi_{p1}x_{ip}$$

subject to：$$\sum_{j=1}^{p}\phi_{j1}^2 = 1 $$

The vector defines a direction in feature space along which the data vary the most.  

If we project the n data points onto this direction, the projected values are the principal component scores.


**Applications:**

we can adapt regression, classification, and clustering methods by using the first K<< p principal component score vectors as features, which will lead to much less noisy results. (measure of Multicollinearity)

Other applications include data compression: for example, we can take the first few principal components of image data to compress image files.

**Limitation:**

Sometime the variance of the data may not be a good measurement of our interest of the data. Because PCA choose the direction in feature space along which the data vary the most.  

**Difference of PCA and LDA**

- LDA is a supervised model, PCA is a unsupervised model

- LDA reduces K to k-1, but PCA does not have the limitation.

- LDA chooses the projection that has the best classification ability, but PCA choose the direction in feature space along which the data vary the most.  

**Is orthogonal necessary in PCA?**

Yes, because in PCA, we aim to select fewer components (than features) which can explain the maximum variance in the data set, and by doing orthogonal it will maximize the difference between variance captured by the component.

**What will happen if you don’t rotate the components?**

If we don’t rotate the components, the effect of PCA will diminish and we’ll have to select more number of components to **explain** variance in the data set.


## 4. What cross validation technique would you use on time series data set?

We will not use regular cross validation technique to deal with time series.

In time series problem, traditional cross validation can be troublesome because there might be some pattern in year 4 or 5 which is not in year 3. Resampling the data set will separate these trends, and we might end up validation on past years, which is incorrect.
 
Instead, Here is one way I will use forward chaining strategy with 5 fold as shown below:
fold 1 : training [1], test [2]
fold 2 : training [1 2], test [3]
fold 3 : training [1 2 3], test [4]
fold 4 : training [1 2 3 4], test [5]
fold 5 : training [1 2 3 4 5], test [6]
where 1,2,3,4,5,6 represents “year”.

## 5. How is KNN different from k-means clustering?

K-Nearest Neighbors is a supervised classification algorithm, while k-means clustering is an unsupervised clustering algorithm. 

While the mechanisms may seem similar at first, what this really means is that in order for K-Nearest Neighbors to work, you need labeled data you want to classify an unlabeled point into (thus the nearest neighbor part). 

K-means clustering requires only a set of unlabeled points and a threshold: the algorithm will take unlabeled points and gradually learn how to cluster them into groups by computing the mean of the distance between different points.

## 6. What’s the “kernel trick” and how is it useful?

Kernel trick:
Kernel functions can enable in higher-dimension spaces without explicitly calculating the coordinates of points within that dimension: instead, kernel functions compute the inner products between the images of all pairs of data in a feature space.

Why it is useful:
It can calculate the coordinates of higher dimensions while being computationally cheaper than the explicit calculation of said coordinates. Many algorithms can be expressed in terms of inner products. Using the kernel trick enables us effectively run algorithms in a high-dimensional space with lower-dimensional data.

## 


