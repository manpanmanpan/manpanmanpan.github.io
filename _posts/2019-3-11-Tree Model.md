---
layout:     post
title:      Tree Model
subtitle:   Decision Tree, Random Forest, Bagging, Boosting
date:       2019-3-11
author:     Cassie Pan
header-img: img/post-bg-rwd.jpg 
catalog: true
tags:
    - ID3, C4.5, CART, Adaboosting, Gradient Boosting, Random Forest
---


## 1. Decision Tree

### 1.1 ID3 (Classification)

**Information Gain**: choose feature has max information gain as split condition.

### 1.2 C4.5 (Regression and Classification)

**Gain Ratio**: choose feature has max gain ratio as split condition.

### 1.3. CART (Regression and Classification)

**Gini Index**: choose a feature that minimizes the Gini index after division by that feature.
Gini index is as a measure of deviation from perfect equality.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552342459(1).jpg?raw=true)

#### Advantages and Disadvantages of Trees

▲ Easier to explain 

▲ More closely mirror humanndecision-making 

▲ Trees can be displayed graphically, and are easily interpreted

▲ Trees can easily handle qualitative predictors without the need to create dummy variables

▼ Unfortunately, trees generally do not have the same level of predictive accuracy as some of the other regression and classification approaches

▼ Additionally, trees can be very non-robust. A small change in the data can cause a large change in the final estimated tree


## 2. Bagging

We bootstrap, by taking repeated samples from the (single) training data set. In this approach we generate B different bootstrapped training data sets. We then train our method on the $b_th$ bootstrapped training set in order to get $\hat{f}^{*b}(x)$, and finally average all the predictions, to obtain:

$$ \hat{f}_{bag}(x) = \frac{1}{B}\sum_{b=1}^B\hat{f}^{*b}(x) $$

This is called bagging. Each tree is built on a bootstrap data set, independent of the other trees. The number of trees B is not a critical parameter with bagging; Using a very large value of B will **not lead to overfitting**.

### 2.2 Out-of-Bag Error Estimation

For Example, each bagged tree makes use of around two-thirds of the observations. The remaining one-third of the observations not used to fit a given bagged tree are referred to as the out-of-bag (OOB) observations.

The resulting OOB error is a valid estimate of the test error for the bagged model, since the response for each observation is predicted using only the trees that were not fit using that observation. With B sufficiently large, OOB error is virtually equivalent to leave-one-out cross-validation error. The OOB approach for estimating the test error is particularly convenient when performing bagging on large data sets for which cross-validation would be computationally onerous.

#### Any pros and cons in practical implementation?


## 3. Random Forests

Random forests provide an improvement over bagged trees by way of a random small tweak that decorrelates the trees.

Each time a split in a tree is considered, a random sample of m predictors is chosen as split candidates from the full set of p predictors. The split is allowed to use only one of those m predictors. A fresh sample of
m predictors is taken at each split, and typically we choose $ m ≈ \sqrt{p} $

#### Why Random Forests?

Suppose that there is one very strong predictor in the data set, along with a number of other moderately strong predictors. Then in the collection of bagged trees, most or all of the trees will use this strong predictor in the top split.
Consequently, all of the bagged trees will look quite similar to each other.
Hence the predictions from the bagged trees will be highly correlated. Unfortunately, averaging many highly correlated quantities does not lead to
as large of a reduction in variance as averaging many uncorrelated quantities.
Random forests overcome this problem by forcing each split to consider only a subset of the predictors.

As with bagging, random forests will **not overfit** if we increase B.


#### Any pros and cons in practical implementation?


## 4. Boosting

Boosting works in a similar way as Bagging, except that the trees are grown sequentially: each tree is grown using information from previously grown trees. Boosting does not involve bootstrap sampling; instead each
tree is fit on a modified version of the original data set.

Note that in boosting, the construction of each tree depends strongly on the trees that have already been grown.

In boosting, because the growth of a particular tree takes into account the other trees that have already been grown, smaller trees are typically sufficient. Using smaller trees can **aid in interpretability** as well; for instance, using stumps leads to an **additive** model.

### 4.1 AdaBoosting

[AdaBoost Tutorial](http://mccormickml.com/2013/12/13/adaboost-tutorial/)

**Note**: In this paper, the outputs are limited to -1 or +1.

#### 4.1.1 How do we select the training set?

Each weak classifier should be trained on a random subset of the total training set. The subsets can overlap. AdaBoost assigns a “weight” to each training example, which determines the probability that each example should appear in the training set. Examples with higher weights are more likely to be included in the training set, and vice versa. After training a classifier, AdaBoost increases the weight on the misclassified examples so that these examples will make up a larger part of the next classifiers training set, and hopefully the next classifier trained will perform better on them.

#### 4.1.2 How to assign weight to each classifier?

The classifiers are trained one at a time. After each classifier is trained, we update the probabilities of each of the training examples appearing in the training set for the next classifier.

The first classifier (t = 1) is trained with equal probability given to all training examples. After it’s trained, we compute the output weight (alpha) for that classifier.

$$ \alpha = \frac{1}{2}ln(\frac{1-\epsilon_t}{\epsilon_t})$$

$\epsilon_t$ is just the number of misclassifications over the training set divided by the training set size.

![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552463193(1).png?raw=true)

From the plot:

- The classifier weight grows exponentially as the error approaches 0. Better classifiers are given exponentially more weight.

- The classifier weight is zero if the error rate is 0.5. A classifier with 50% accuracy is no better than random guessing, so we ignore it.

- The classifier weight grows exponentially negative as the error approaches 1. We give a negative weight to classifiers with worse worse than 50% accuracy. “Whatever that classifier says, do the opposite!”.


#### 4.1.3 How to assign weight to each observation?

Then, we need to update the training example weights ($D(i)$):

$$ D_{t+1}(i)= \frac{D_t(i)exp(-\alpha_ty_ih_t(x_i))}{Z_t}$$


The variable $D_t$ is **a vector of weights**, with one weight for each training example in the training set. ‘i’ is the training example number. This equation shows you how to update the weight for the $i_{th}$ training example. Each weight $D(i)$ represents the probability that training example i will be selected as part of the training set.

$y_i$ is the true value, $h_t(x_i)$ is the predicted value ($\hat{y_i}$), $Z_t$ is the sum of all the weights, in order to normalize $D_{t+1}$, let $\sum_{i}{D_{t+1}(i)} = 1$.

Note: if $y_i = \hat{y_i}, ~~y_ih_t(x_i)$ always be 1, so $yh(x)$ only contribute to sign not the magnitute.

##### Why use the function of exp(x)?
![image](https://github.com/manpanmanpan/manpanmanpan.github.io/blob/master/img/1552521610(1).jpg?raw=true)

From the plot, we see:
if $ x<0$, $exp(x)$ returns a fraction between 0, 1;
if $ x>0$, $exp(x)$ returns a value greater than 1.
So the weight for training sample i will be eigher increased or decreased depending on the final sign of the term "$-\alpha yh(x)$".

Assume a useful tree ($\alpha_t >0$):
If $yh(x)$ = -1, which means misclassification, $-\alpha y_i h_t(x_i)$ would be positive, $exp(-\alpha y_i h_t(x_i))$ returns a value greater than 1. Thus, this training smaple i to be given a larger weight, which would have a high prob to be selected for following classifier tree. We hope the next classifier trains better on it.

Note that by including alpha in this term, we are also incorporating the classifier’s effectiveness into consideration when updating the weights. If a weak classifier misclassifies an input, we don’t take that as seriously as a strong classifier’s mistake.

#### 4.1.4 How to combine each classifier?

After each classifier is trained, the classifier’s weight is calculated based on its accuracy. More accurate classifiers are given more weight. A classifier with 50% accuracy is given a weight of zero, and a classifier with less than 50% accuracy is given negative weight.

Our final classifier:

$$ H(x) = sign(\sum_{t=1}^{T}\alpha_th_t(x))$$

$h_t(x)$ is the output of weak classifier t. $\alpha_t$ is the weight applied to classifier t as determined by AdaBoost. So the final output is just a linear combination of all of the weak classifiers, and then we make our final decision simply by looking at the sign of this sum.


### 4.2 Gradient Boosting


#### Any pros and cons in practical implementation?

 