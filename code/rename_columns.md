---
layout: archive
title: "Rename Columns in a Pandas DataFrame"
permalink: /code/rename_columns_pandas_dataframe
author_profile: true
redirect_from:
  - /rename_column
---

{% include base_path %}

There are two easy ways to rename one or more columns in a Pandas DataFrame. This post shows both methods with some example data.

# Imports
```python
import pandas as pd
```

# Create Some Example Data

Say somebody sends you a file with three columns representing people's name, age, and sex. The file is sent with these columns named `a`, `b`, and `c`. These aren't useful column names; you'll want to rename them to something more descriptive. 

```python
data = {"a": ["James", "Alice", "Phil", "James"],
		"b": [24, 28, 40, 24],
		"c": ["Male", "Female", "Male", "Male"]}
df = pd.DataFrame(data)
print(df)
```

**a**|**b**|**c**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male
James|24|Male

# Rename Columns Using the Replace Function

The most flexible way to rename columns is to use Pandas' `df.replace` function. It can take as arguments either a dictionary of `{old_name: new_name}` pairs, or a function that you want to apply to all columns. An example of both:

```python
# rename columns using a dictionary mapping old to new names
df_using_dict = df.rename(columns={'a': 'Name', 'b': 'Age', 'c': 'Sex'})
print(df_using_dict)

# make all column names uppercase using a function
df_using_function = df.rename(str.upper, axis='columns')
print(df_using_function)
```

**Name**|**Age**|**Sex**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male
James|24|Male

**A**|**B**|**C**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male
James|24|Male

Note that when applying a function to all column names instead of directly mapping them with a dictionary, you need to specify `axis=columns` so that Pandas knows to apply the function to column names rather than row indexes.

One nice trait about `rename` is that you can pick and choose which columns to apply it to. If you want to rename a small subset of columns, this is your easiest way of doing so. 

# Rename Columns Using df.columns

A second common way of renaming columns is by assigning a new list of values to `df.columns`.


```python
# replace old column names with new ones by assigning a list of names to df.columns
df.columns = ['Name', 'Age', 'Sex']
print(df)
```

**Name**|**Age**|**Sex**
:-----:|:-----:|:-----:
James|24|Male
Alice|28|Female
Phil|40|Male
James|24|Male

This approach is usually more labor-intensive because it requires you to specify the entire list of new column names, whereas the replace function lets you specify as few or as many columns as you wish.


