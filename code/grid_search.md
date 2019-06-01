---
layout: archive
title: "Tune Hyperparameters with Grid Search"
permalink: /code/grid_search
author_profile: true
date: 2019-06-01
redirect_from:
  - /grid_search
---

{% include base_path %}

In this post I'll show a full example of how to tune a model's hyperparameters using Scikit-Learn's grid search implementation `GridSearchCV`.

# Background

Grid search is a common method for tuning a model's hyperparameters. The grid search algorithm is simple: you feed it a set of hyperparameters and the values you want to test for each hyperparameter, and then run an exhaustive search over all possible combinations of these values, training one model for each set of values. The algorithm then compares the scores of each model it trains and keeps the best one. A common extension of grid search is to use it alongside cross validation, training on several different folds for each hyperparameter combination to have a more reliable estimate of each model's performance out of sample. For notes on cross validation, see [here](https://jamesrledoux.com/code/k_fold_cross_validation).

# Setup: Imports, Data Acquisition

I'll use the Iris dataset because it's easy to import from Scikit-Learn. The model we tune using grid search will be a random forest classifier.

```python
# import random search, random forest, and iris data
from sklearn.model_selection import GridSearchCV
from sklearn import datasets
from sklearn.ensemble import RandomForestClassifier

# get iris data
iris = datasets.load_iris()
X = iris.data
y = iris.target
```

# Set Up a Grid of Hyperparameter Values

I'll tune three hyperparameters: `n_estimators`, `max_features`, and `min_samples_split`. For each parameter I'll need to form a hypothesis about which values I think will work in the model; you need to explicitly state each value you want grid search to test.  

The hyperparameter values are set up as a dictionary so they can be passed to `GridSearchCV`.

```python
model_params = {
    'n_estimators': [50, 150, 250],
    'max_features': ['sqrt', 0.25, 0.5, 0.75, 1.0],
    'min_samples_split': [2, 4, 6]
}
```

# Define and Train the Model with Grid Search

The most important arguments to pass to `GridSearchCV` are the model you're training, the dictionary of parameter values you're testing, and the number of folds for it to cross validate over. 

The grid search meta-estimator runs an exhaustive search over all possible combinations of the hyperparameter values you pass to it. The number of cross validation folds you choose determines how many times it will train each model on a different subset of data in order to assess model quality.

The result of training the grid search meta-estimator will be the best model that it finds across all candidate models. 

```python
# create random forest classifier model
rf_model = RandomForestClassifier(random_state=1)

# set up grid search meta-estimator
clf = GridSearchCV(rf_model, model_params, cv=5)

# train the grid search meta-estimator to find the best model
model = clf.fit(X, y)

# print winning set of hyperparameters
from pprint import pprint
pprint(model.best_estimator_.get_params())
```

```
{'bootstrap': True,
 'class_weight': None,
 'criterion': 'gini',
 'max_depth': None,
 'max_features': 'sqrt',
 'max_leaf_nodes': None,
 'min_impurity_decrease': 0.0,
 'min_impurity_split': None,
 'min_samples_leaf': 1,
 'min_samples_split': 2,
 'min_weight_fraction_leaf': 0.0,
 'n_estimators': 50,
 'n_jobs': 1,
 'oob_score': False,
 'random_state': 1,
 'verbose': 0,
 'warm_start': False}
 ```

There are several hyperparameters that I chose not to tune in this example, but of the ones we did tune, the winning values of `max_features`, `n_estimators`, and `min_samples_split` were 'sqrt', 50, and 2 respectively. 

# Generate Predictions Using the Best Model

Now that you have a tuned model, there's no additional work needed to generate predictions from the best model that grid search found. Simply call `.predict()` on the meta-estimator and you're good to go. 

```python
# generate predictions using the best-performing model
predictions = model.predict(X)
print(predictions)
```

`[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2
 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
 2 2]`

# Closing Comments

Grid search is a useful algorithm for tuning model parameters and improving overall model quality. That said, you will usually get better results using [random search](https://jamesrledoux.com/code/randomized_parameter_search). Grid search will only explore the hyperparameter values you tell it to use, while random search is able to draw hyperparameter values from continuous distributions, allowing it to sample the parameter space more fully and efficiently.

Grid search is also an epensive algorithm. You'll want to choose your parameter values carefully. For each additional value you add to your grid search for one hyperparameter, the algorithm will train it against all other possible values of all the other parameters you're tuning. Paired with 5-fold cross validation, it will do this five times. This can quickly spiral out of control into a model that never finishes training.

The last thing I'll note is that it's admittedly silly to tune parameters in this way on the Iris dataset. The purpose of this post is to show how to apply grid search in a way that generalizes to as many use cases as possible, and Iris is an easy-to-access dataset that's fast to train on. Happy tuning!




















