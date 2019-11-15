---
layout: archive
title: "Drop Columns in a Pandas DataFrame"
permalink: /code/drop_columns
author_profile: true
date: 2019-06-01
last_modified_at: 2019-06-01	
redirect_from:
  - /drop_columns
---

{% include base_path %}
This post shows how to drop one or more columns from a Pandas DataFrame using `df.drop`. 

# Imports
```python
import pandas as pd
```

# Create Example Data

The following DataFrame has three columns: Name, Age, and Sex. 

```python
data = {"Name": ["James", "Alice", "Phil", "James"],
		"Age": [24, 28, 40, 24],
		"Sex": ["Male", "Female", "Male", "Male"]}
df = pd.DataFrame(data)
print(df)
```

**Name**|**Age**|**Sex**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male
James|24|Male

# Drop One Column

`df.drop` accepts two arguments: the name of the column you're dropping, and the axis. The axis argument is always equal to 1 when dropping columns. Dropping the Age column would look like this:

```python
df_without_age = df.drop('Age', 1)
print(df_without_age)
```

**Name**|**Sex**
:-----:|:-----:
James|Male
Alice|Female
Phil|Male

# Drop Multiple Columns

Dropping multiple columns has similar syntax to dropping a single column. The only difference is that you pass a list of column names rather than a single string value. Here's how you would drop both the Age and Sex columns in a single command:

```python
df_without_age_or_sex = df.drop(['Age', 'Sex'], 1)
print(df_without_age_or_sex)
```

**Name**|
:-----:|
James|
Alice|
Phil|

One additional trick is that you can do this in place without assigning the DataFrame you just dropped a column from to a new or existing variable. To do this, specify `inplace=True` inside the `df.drop` command. 

### Want to improve your Python skills? I recommend reading [Python for Data Analysis by Wes McKinney](https://www.amazon.com/gp/product/1491957662/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491957662&linkCode=as2&tag=ledoux-20&linkId=eff92247940c967299befaed855c580a), the creator of Pandas

![Python for Data Analysis book cover](https://images-na.ssl-images-amazon.com/images/I/51cUNf8zukL._SX379_BO1,204,203,200_.jpg)

[Get it on Amazon here for $36.26](https://www.amazon.com/gp/product/1491957662/ref=as_li_tl_nodl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491957662&linkCode=as2&tag=ledoux-20&linkId=eff92247940c967299befaed855c580a)

