---
layout: archive
title: "Create Dummy Variables in Pandas"
permalink: /code/dummies
author_profile: true
redirect_from:
  - /dummies
---

{% include base_path %}

This post shows how to create dummy variables using Pandas' `pd.get_dummies` function.

# Background

A dummy variable is a binary variable that indicates whether a separate categorical variable takes on a specific value. For a categorical variable that takes on more than one value, it is useful to create one dummy variable for each unique value that the categorical variable takes on. Here's how you can do that in Python:

# Imports
```python
import pandas as pd
```

# Create a Toy Dataset
```python
data = {"Name": ["James", "Alice", "Phil"],
		"Age": [24, 28, 40],
		"Sex": ["Male", "Female", "Male"]}
df = pd.DataFrame(data)
print(df)
```

**Name**|**Age**|**Sex**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male

# Create Dummy Variables
Create dummy variables with Pandas' `get_dummies` function. You will often be creating dummies for several different categorical features in your dataset, so I like to add a descriptive prefix to my dummy columns' names. The example works fine without the `.rename()` at the end of this example, though, so feel free to omit it if it doesn't help.

```python
# create dummies for pitching team, batting team, pitcher id, batter id
dummies = pd.get_dummies(df['Sex']).rename(columns=lambda x: 'Sex_' + str(x))
# bring the dummies back into the original dataset
df = pd.concat([df, dummies], axis=1)
print(df)
```

 |**Name**|**Age**|**Sex**|**Sex\_Female**|**Sex\_Male**
:-----:|:-----:|:-----:|:-----:|:-----:
James|24|Male|0|1
Alice|28|Female|1|0
Phil|40|Male|0|1
