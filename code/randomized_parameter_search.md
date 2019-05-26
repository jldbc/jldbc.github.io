---
layout: archive
title: "Tune Hyperparameters with Randomized Search"
permalink: /code/randomized_parameter_search
author_profile: true
redirect_from:
  - /randomized_search
---

{% include base_path %}

This post shows how to apply randomized hyperparameter search to an example dataset using Scikit-Learn's implementation of RandomizedSearchCV (randomized search cross validation).

# Background

The most efficient way to find an optimal set of hyperparameters for a machine learning model is to use random search. The randomized search meta-estimator is an algorithm that trains and evaluates a series of models by taking random draws from a predetermined set of hyperparameter distributions. The algorithm picks the most successful version of the model it's seen after training N different versions of the model with different randomly selected hyperparameter combinations, leaving you with a model trained on a near-optimal set of hyperparameters. Note that random search is called a meta-estimator because it's not an estimator in itself, but rather an algorithm applied to an existing estimator in order to tune the estimator's hyperparameters.

This method has an advantage over grid search in that the algorithm searches over distributions of parameter values rather than predetermined lists of candidate values for each hyperparameter. Being able to search over hyperparameter distributions also allows you to be more opinionated about what you expect a hyperparameter's best value to be; if you want to draw values from a distribution that is normally, poisson, uniformly distributed, etc., you can specify it as such. 

Random search is usually used in tandem with cross validation to achieve a more reliable estimate of what each candidate model's out of sample performance will be. For notes on cross validation, see [here](https://jamesrledoux.com/code/k_fold_cross_validation).

# Setup: Imports, Data Acquisition

I'll use the Iris dataset because it's easy to import from Scikit-Learn. The model we tune using random search will be a random forest classifier. We will specify three different types of parameter distribution to search through: uniform, random integer, and truncated normal, all implemented using scipy. 

```python
# import random search, random forest, iris data, and distributions
from sklearn.model_selection import RandomizedSearchCV
from sklearn import datasets
from sklearn.ensemble import RandomForestClassifier
from scipy.stats import uniform, truncnorm, randint

# get iris data
iris = datasets.load_iris()
X = iris.data
y = iris.target
```

# Set Up Hyperparameter Distributions

I'll tune three hyperparameters: `n_estimators`, `max_features`, and `min_samples_split`. `n_estimators` is an integer and I don't know what will work best, so for this I'll define its distribution using `randomint`. `max_features` takes a float value and I think the best value will be in the neighborhood of using 25% of the data's features, so I'll define this as a truncated normal distribution to favor values closer to 0.25 while staying between zero and one. I don't know what will work best for `min_samples_split`, so I'll use a uniform distribution from 0.1 to 20% of observations. 

The hyperparameter distributions are set up as a dictionary so they can be passed to `RandomizedSearchCV`.

```python
model_params = {
    # randomly sample numbers from 4 to 204 estimators
    'n_estimators': randint(4,200),
    # normally distributed max_features, with mean .25 stddev 0.1, bounded between 0 and 1
    'max_features': truncnorm(a=0, b=1, loc=0.25, scale=0.1),
    # uniform distribution from 0.01 to 0.2 (0.01 + 0.199)
    'min_samples_split': uniform(0.01, 0.199)
}
```

# Define and Train the Model with Random Search

The most important arguments to pass to `RandomizedSearchCV` are the model you're training, the dictionary of parameter distributions, the number of iterations for random search to perform, and the number of folds for it to cross validate over. 

Each iteration represents a new model trained on a new draw from your dictionary of hyperparameter distributions. The number of cross validation folds you choose determines how many times it will train each model on a different subset of data in order to assess model quality. The total number of models random search trains is then equal to `n_iter * cv`.

The result of training the randomized search meta-estimator will be the best model that it found from all `n_iter` candidate models. 

```python
# create random forest classifier model
rf_model = RandomForestClassifier()

# set up random search meta-estimator
# this will train 100 models over 5 folds of cross validation (500 models total)
clf = RandomizedSearchCV(rf_model, model_params, n_iter=100, cv=5, random_state=1)

# train the random search meta-estimator to find the best model out of 100 candidates
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
 'max_features': 0.34317084571422385,
 'max_leaf_nodes': None,
 'min_impurity_decrease': 0.0,
 'min_impurity_split': None,
 'min_samples_leaf': 1,
 'min_samples_split': 0.10811885911540445,
 'min_weight_fraction_leaf': 0.0,
 'n_estimators': 132,
 'n_jobs': 1,
 'oob_score': False,
 'random_state': None,
 'verbose': 0,
 'warm_start': False}
 ```

There are several hyperparameters that I chose not to tune in this example, but of the ones we did tune, the winning values of `max_features`, `n_estimators`, and `min_samples_split` were 0.343, 132, and 0.108 respectively. 

# Generate Predictions Using the Best Model

Now that you have a tuned model, there's no additional work needed to generate predictions from the best model that randomized search found. Simply call `.predict()` on the meta-estimator and you're good to go. 

```python
# generate predictions using the best-performing model
predictions = model.predict(X)
print(predictions)
```

`[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 1 1 1
 1 1 1 1 1 1 1 1 1 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 1 2 2 2 2
 2 2 2 2 2 2 2 2 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
 2 2]`

 The last thing I'll note is that it's admittedly silly to tune parameters in this way on the Iris dataset. The purpose of this post is to show how to apply random search in a way that generalizes to as many use cases as possible, and Iris is an easy-to-access dataset that's fast to train on. Happy tuning!