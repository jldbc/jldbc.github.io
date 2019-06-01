---
layout: archive
title: "Drop Duplicate Rows in a DataFrame"
permalink: /code/drop_duplicates
author_profile: true
date: 2019-06-01
redirect_from:
  - /duplicates
---

{% include base_path %}
This post shows how to remove duplicate records and combinations of columns in a Pandas dataframe and keep only the unique values. 

# Imports
```python
import pandas as pd
```

# Create Example Data
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

# Drop Duplicate Rows

`drop_duplicates` returns only the dataframe's unique values. Removing duplicate records is sample.

```python
df = df.drop_duplicates()
print(df)
```

**Name**|**Age**|**Sex**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male

To remove duplicates of only one or a subset of columns, specify `subset` as the individual column or list of columns that should be unique. To do this conditional on a different column's value, you can `sort_values(colname)` and specify `keep` equals either `first` or `last`. 

In our example data, this could be useful if we had two entries for Name = James, one with Age = 24 and one with Age = 25. If we know we only want the oldest example for each person, we can sort by Age and drop duplicates of the name column, keeping only the observation with the highest age. 

```python
data = {"Name": ["James", "Alice", "Phil", "James"],
		"Age": [24, 28, 40, 25],
		"Sex": ["Male", "Female", "Male", "Male"]}
df = pd.DataFrame(data)
print(df)
```

**Name**|**Age**|**Sex**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male
James|25|Male

```python
df = df.sort_values('Age', ascending=False)
df = df.drop_duplicates(subset='Name', keep='first')
print(df)
```

**Name**|**Age**|**Sex**
:-----:|:-----:|:-----:
Phil|40|Male
Alice|28|Female
James|25|Male

Despite the full records not being duplicated, our duplicatation problem is once again resolved.










