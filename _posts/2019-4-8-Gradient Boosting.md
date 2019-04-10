---
layout:     post
title:      Gradient Boosting
subtitle:   
date:       2019-4-8
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    -  
---

# Gradient boosting involves three elements:

- **A loss function to be optimized.**
- **A weak learner to make predictions.**
- **An additive model to add weak learners to minimize the loss function.**


## 1. Loss Function

The loss function must be differentiable.

For example, regression may use a squared error and classification may use logarithmic loss.

A benefit of the gradient boosting framework is that a new boosting algorithm does not have to be derived for each loss function that may want to be used, instead, it is a generic enough framework that any differentiable loss function can be used.


## 2. Weak Learner

Decision trees are used as the weak learner in gradient boosting.

Specifically regression trees are used that output real values for splits and whose output can be added together, allowing subsequent models outputs to be added and “correct” the residuals in the predictions.

Trees are constructed in a greedy manner, choosing the best split points based on purity scores like Gini or to minimize the loss.

Initially, such as in the case of AdaBoost, very short decision trees were used that only had a single split, called a decision stump. Larger trees can be used generally with 4-to-8 levels.

It is common to constrain the weak learners in specific ways, such as a maximum number of layers, nodes, splits or leaf nodes.

This is to ensure that the learners remain weak, but can still be constructed in a greedy manner.

## 3. Additive Model

Trees are added one at a time, and **existing trees in the model are not changed.**

A gradient descent procedure is used to minimize the loss when adding trees.

Traditionally, gradient descent is used to minimize a set of parameters, such as the coefficients in a regression equation or weights in a neural network. After calculating error or loss, the weights are updated to minimize that error.

Instead of parameters, we have weak learner sub-models or more specifically decision trees. After calculating the loss, to perform the gradient descent procedure, we must add a tree to the model that reduces the loss (i.e. follow the gradient). We do this by parameterizing the tree, then modify the parameters of the tree and **move in the right direction** by reducing the residual loss.

Generally this approach is called functional gradient descent or gradient descent with functions.

The output for the new tree is then added to the output of the existing sequence of trees in an effort to correct or improve the final output of the model.

A fixed number of trees are added or training stops once loss reaches an acceptable level or no longer improves on an external validation dataset.


## 4. Difference between AdaBoost and Gradient Boosting

 The major difference between AdaBoost and Gradient Boosting Algorithm is how the two algorithms identify the shortcomings of weak learners (eg. decision trees). While the AdaBoost model identifies the shortcomings by using high weight data points, gradient boosting performs the same by using gradients in the loss function (y=ax+b+e , e needs a special mention as it is the error term).

## 5. Improvements to Basic Gradient Boosting (reducing overfitting)


### 5.1 Tree Constraints

- **Number of trees**, generally adding **more trees** to the model can be very slow to overfit. The advice is to keep adding trees until no further improvement is observed.

- **Tree depth**, deeper trees are more complex trees and shorter trees are preferred. Generally, better results are seen with 4-8 levels.

- **Number of nodes or number of leaves**, like depth, this can constrain the size of the tree, but is not constrained to a symmetrical structure if other constraints are used.

- **Number of observations per split** imposes a minimum constraint on the amount of training data at a training node before a split can be considered.

- **Minimim improvement to loss** is a constraint on the improvement of any split added to a tree.

### 5.2 Weighted Updates (Shrinkage)

The predictions of each tree are added together sequentially.

The contribution of each tree to this sum can **be weighted** to slow down the learning by the algorithm. This weighting is called **a shrinkage or a learning rate**. Each update is simply scaled by the value of the “learning rate parameter v”.

The effect is that learning is slowed down, in turn require more trees to be added to the model, in turn taking longer to train, providing a configuration **trade-off between the number of trees and learning rate.** Decreasing the value of v [the learning rate] increases the best value for M [the number of trees].

It is common to have small values in the range of 0.1 to 0.3, as well as values less than 0.1.

shrinkage reduces the influence of each individual tree and leaves space for future trees to improve the model.

### 5.3  Stochastic Gradient Boosting

A few variants of stochastic boosting that can be used:

- Subsample rows before creating each tree.
- Subsample columns before creating each tree
- Subsample columns before considering each split.

Generally, aggressive sub-sampling such as selecting only 50% of the data has shown to be beneficial.

At each iteration a subsample of the training data is drawn at random (without replacement) from the full training dataset. The randomly selected subsample is then used, instead of the full sample, to fit the base learner.

According to user feedback, using column sub-sampling prevents over-fitting even more so than the traditional row sub-sampling.

### 5.4 Penalized Gradient Boosting

Additional constraints can be imposed on the parameterized trees in addition to their structure.

Classical decision trees like CART are not used as weak learners, instead a modified form called a regression tree is used that has numeric values in the leaf nodes (also called terminal nodes). The values in the leaves of the trees can be called weights in some literature.

As such, the leaf weight values of the trees can be regularized using popular regularization functions, such as:

L1 regularization of weights.
L2 regularization of weights.
The additional regularization term helps to smooth the final learnt weights to avoid over-fitting. Intuitively, the regularized objective will tend to select a model employing simple and predictive functions.



[A Gentle Introduction to the Gradient Boosting Algorithm for Machine Learning](https://machinelearningmastery.com/gentle-introduction-gradient-boosting-algorithm-machine-learning/)