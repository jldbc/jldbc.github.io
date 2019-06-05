---
layout: archive
title: "Breaking Data into a Train and Test Set"
permalink: /code/train_test_split
author_profile: true
date: 2019-06-01
last_modified_at: 2019-06-01
redirect_from:
  - /train_test_split
---

{% include base_path %}

# Imports

```python
import pandas as pd
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
```

# Load Data
```python
# load the iris dataset and get X and Y data
iris = load_iris()
X = pd.DataFrame(iris.data)
y = pd.DataFrame(iris.target)
```

# Split Data into Train and Test Set
```python
# set aside 20% of train and test data for evaluation
X_train, X_test, y_train, y_test = train_test_split(X, y,
    test_size=0.2, shuffle = True, random_state = 123)
print("X_train shape: {}".format(X_train.shape))
print("X_test shape: {}".format(X_test.shape))
print("y_train shape: {}".format(y_train.shape))
print("y_test shape: {}".format(y_test.shape))
 ```

`X_train shape: (120, 4)`

`X_test shape: (30, 4)`

`y_train shape: (120, 1)`

`y_test shape: (30, 1)`

