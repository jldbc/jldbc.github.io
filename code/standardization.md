---
layout: archive
title: "Standardizing Features"
permalink: /code/standardization
author_profile: true
redirect_from:
  - /standardization
---

{% include base_path %}

Machine learning models can be sensitive to the magnitude of their inputs. If one or several features in your data are of a larger magnitude than the rest, they may have undue influence over the model's output. Scaling your features to have similar magnitude can help models to better generalize and converge faster.

# Imports
```python
import pandas as pd
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import MinMaxScaler
```

# Generate Data
```python
# create two similar features with different scales
df = pd.DataFrame({"X1": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
	"X2": [0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100]})
print(df)
```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|0|0
1|1|10
2|2|20
3|3|30
4|4|40
5|5|50
6|6|60
7|7|70
8|8|80
9|9|90
10|10|100

# Method 1: StandardScaler
This method scales all features to have a mean of 0 and variance of 1. This is my scaler of choice in most cases because it standardizes both magnitude and variance. 

## Fit the Scaler and Apply its Transformation
```python
# save column names before transforming because standardscaler throws them out
cols = df.columns
df_scaled = pd.DataFrame(StandardScaler().fit_transform(df))
df_scaled.columns = cols
print(df_scaled)
 ```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|-1.581139|-1.581139
1|-1.264911|-1.264911
2|-0.948683|-0.948683
3|-0.632456|-0.632456
4|-0.316228|-0.316228
5|0.000000 |0.000000
6|0.316228|0.316228
7|0.632456|0.632456
8|0.948683|0.948683
9|1.264911|1.264911
10|1.581139|1.581139


# Method 2: Min-Max Scaler
This method scales all features to have the same minimum and maximum values. Common min/max values for this are 0 and 1. 

## Fit the Scaler and Apply its Transformation
```python
# save column names before transforming because standardscaler throws them out
cols = df.columns
df_scaled = pd.DataFrame(MinMaxScaler(feature_range=(0, 1)).fit_transform(df))
df_scaled.columns = cols
print(df_scaled)
 ```

**idx**|**X1**|**X2**
:-----:|:-----:|:-----:
0|0.0|0.0
1|0.1|0.1
2|0.2|0.2
3|0.3|0.3
4|0.4|0.4
5|0.5|0.5
6|0.6|0.6
7|0.7|0.7
8|0.8|0.8
9|0.9|0.9
10|1.0|1.0




