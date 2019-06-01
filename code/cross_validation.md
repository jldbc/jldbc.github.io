---
layout: archive
title: "K-Fold Cross Validation"
permalink: /code/k_fold_cross_validation
author_profile: true
date: 2019-06-01
redirect_from:
  - /cross_validation
---

{% include base_path %}

This post shows how to apply k-fold cross validation using Scikit-Learn.

# Background

K-fold cross validation works by breaking your training data into K equal-sized "folds." It iterates through each fold, treating that fold as holdout data, training a model on all the other K-1 folds, and evaluating the model's performance on the one holdout fold. This results in having K different models, each with an out of sample model accuracy score on a different holdout set. The average of these K models' out-of-sample scores is the model's cross-validation score.

Cross validation is useful because it provides a lower-variance estimate of the model's true out of sample score than if you had only used a single train-test split.

# Setup: Imports, Data Acquisition

I'll use the Iris dataset and a random forest classifier for this example. The dataset, model, and cross validation function can all be imported from Scikit-Learn.

```python
# import random search, random forest, iris data, and distributions
from sklearn.model_selection import cross_validate
from sklearn import datasets
from sklearn.ensemble import RandomForestClassifier

# get iris data
iris = datasets.load_iris()
X = iris.data
y = iris.target
```

# Train and Evaluate a Model Using K-Fold Cross Validation

Here I initialize a random forest classifier and feed it to sklearn's `cross_validate` function. This function receives a model, its training data, the array or dataframe column of target values, and the number of folds for it to cross validate over (the number of models it will train).

The cross validation object stores the out of sample accuracy of each of its trained models. Taking the average of these K out-of-sample scores gives you the model's cross-validation accuracy, a low-variance estimate of how the model will perform on unseen data.

```python
model = RandomForestClassifier(random_state=1)
cv = cross_validate(model, X, y, cv=5)
print(cv['test_score'])
print(cv['test_score'].mean())
```

`[0.96666667 0.96666667 0.93333333 0.96666667 1.        ]`
`0.9666666666666668`

Cross validation should be used whenever assessing the quality of a model's predictions. It is also baked into common parameter tuning methods such as [grid search cross validation](https://jamesrledoux.com/code/grid_search) and [random search cross validation](https://jamesrledoux.com/code/randomized_parameter_search). 