---
layout: archive
title: "Impute Missing Values"
permalink: /code/imputation
author_profile: true
date: 2019-06-01
redirect_from:
  - /imputation
---

{% include base_path %}

Real world data is filled with missing values. You will often need to rid your data of these missing values in order to train a model or do meaningful analysis. What follows are a few ways to impute (fill) missing values in Python, for both numeric and categorical data.

# Imports
```python
import pandas as pd
import numpy as np
```

# Imputation for Numeric Features
## Create a Toy Dataset

```python
# create two columns of randomly generated values, replace a few examples with NaNs
data = {"X1": [np.nan, 0.7636183 , 0.61735332, 0.73848657, np.nan,
        0.71623709, 0.73075927, np.nan, 0.71073827, 0.54693503],
        "X2": [0.87505771, 0.77210971, 0.64369448, 0.54238232, 0.0710951 ,
        0.6854597 , np.nan, 0.20935994, 0.54764129, np.nan ]}
df = pd.DataFrame(data)
print(df)
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|NaN|0.875058
1|0.763618|0.772110
2|0.617353|0.643694
3|0.738487|0.542382
4|NaN|0.071095
5|0.716237|0.685460
6|0.730759|NaN
7|NaN|0.209360
8|0.710738|0.547641
9|0.546935|NaN

## Imputation Method 1: Mean or Median
A common method of imputation with numeric features is to replace missing values with the mean of the feature's non-missing values. If the data have outliers, you may want to use the median instead. Either method is easy in Pandas:

```python
# replace missing values with the column mean
df_mean_imputed = df.fillna(df.mean())
df_median_imputed = df.fillna(df.median())
df_mean_imputed
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|0.689161|0.875058
1|0.763618|0.772110
2|0.617353|0.643694
3|0.738487|0.542382
4|0.689161|0.071095
5|0.716237|0.685460
6|0.730759|0.543350
7|0.689161|0.209360
8|0.710738|0.547641
9|0.546935|0.543350

## Imputation Method 2: Zero
Depending on where your data are coming from, a missing value may be better represented by the number zero. Replacing missing values with zeros is accomplished similar to the above method; just replace the mean function with zero.

```python
# replace missing values with the column mean
df_zero_imputed = df.fillna(0)
df_zero_imputed
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|0.000000|0.875058
1|0.763618|0.772110
2|0.617353|0.643694
3|0.738487|0.542382
4|0.000000|0.071095
5|0.716237|0.685460
6|0.730759|0.000000
7|0.000000|0.209360
8|0.710738|0.547641
9|0.546935|0.000000


# Imputation for Categorical Data

For categorical features, using mean, median, or zero-imputation doesn't make much sense. Here I'll create an example dataset with categorical features and show two imputation methods specific to this type of data.

## Create a Toy Dataset with Categorical Features
```python
data = {"X1": [np.nan, "Red" , "Blue", "Red", np.nan,
        "Red", "Green", np.nan, "Blue", "Red"],
        "X2": ["Green", "Green", "Red", "Blue", "Green" ,
        "Blue" , np.nan, "Red", "Green", np.nan ]}
colors = pd.DataFrame(data)
print(colors)
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|NaN|Green
1|Red|Green
2|Blue|Red
3|Red|Blue
4|NaN|Green
5|Red|Blue
6|Green|NaN
7|NaN|Red
8|Blue|Green
9|Red|NaN

## Imputation Method 1: Most Common Class
One approach to imputing categorical features is to replace missing values with the most common class. You can do with by taking the index of the most common feature given in Pandas' `value_counts` function. 

```python
# for each column, get value counts in decreasing order and take the index (value) of most common class
df_most_common_imputed = colors.apply(lambda x: x.fillna(x.value_counts().index[0]))
df_most_common_imputed
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|Red|Green
1|Red|Green
2|Blue|Red
3|Red|Blue
4|Red|Green
5|Red|Blue
6|Green|Green
7|Red|Red
8|Blue|Green
9|Red|Green

## Imputation Method 2: "Unknown" Class
Similar to how it's sometimes most appropriate to impute a missing numeric feature with zeros, sometimes a categorical feature's missing-ness itself is valuable information that should be explicitly encoded. If this is the case, most-common-class imputing would cause this information to be lost. Instead, just replace those values with a value like "Unknown" or "Missing."

```python
df_unknown_imputed = colors.fillna("Unknown")
df_unknown_imputed
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|Unknown|Green
1|Red|Green
2|Blue|Red
3|Red|Blue
4|Unknown|Green
5|Red|Blue
6|Green|Unknown
7|Unknown|Red
8|Blue|Green
9|Red|Unknown

# One Final Tip: Column-Specific Imputation Rules
You can combine any of the above methods by imputing specific columns rather than the entire dataframe. Returning to the numeric example, we can mean-impute X1 and median-impute X2 by specifying the column(s) to be imputed. 

```python
# replace missing values with the column mean
df['X1'] = df['X1'].fillna(df['X1'].mean())
df['X2'] = df['X2'].fillna(df['X2'].median())
df
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|0.689161|0.875058
1|0.763618|0.772110
2|0.617353|0.643694
3|0.738487|0.542382
4|0.689161|0.071095
5|0.716237|0.685460
6|0.730759|0.595668
7|0.689161|0.209360
8|0.710738|0.547641
9|0.546935|0.595668


