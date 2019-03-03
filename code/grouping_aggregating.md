---
layout: archive
title: "Group and Aggregate by One or More Columns in Pandas"
permalink: /code/group-by-aggregate-pandas
author_profile: true
redirect_from:
  - /group-by-aggregate-pandas
---

{% include base_path %}

Pandas comes with a whole host of sql-like [aggregation functions](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.agg.html) you can apply when grouping on one or more columns. This is Python's closest equivalent to dplyr's `group_by` + `summarise` logic. Here's a quick example of how to group on one or multiple columns and summarise data with aggregation functions using Pandas. 

# Imports
```python
import pandas as pd
```

# Create a Toy Dataset

In this case, say we have data on baseball players. We know their team, whether they're a pitcher or a position player, and their age. With this data we can compare the average ages of the different teams, and then break this out further by pitchers vs. non-pitchers.

```python
data = {"Team": ["Red Sox", "Red Sox", "Red Sox", "Red Sox", "Red Sox", "Red Sox", "Yankees", "Yankees", "Yankees", "Yankees", "Yankees", "Yankees"],
		"Pos": ["Pitcher", "Pitcher", "Pitcher", "Not Pitcher", "Not Pitcher", "Not Pitcher", "Pitcher", "Pitcher", "Pitcher", "Not Pitcher", "Not Pitcher", "Not Pitcher"],
		"Age": [24, 28, 40, 22, 29, 33, 31, 26, 21, 36, 25, 31]}
df = pd.DataFrame(data)
print(df)
```

**Team**|**Pos**|**Age**
:-----:|:-----:|:-----:
Red Sox|Pitcher|24
Red Sox|Pitcher|28
Red Sox|Pitcher|40
Red Sox|Not Pitcher|22
Red Sox|Not Pitcher|29
Red Sox|Not Pitcher|33
Yankees|Pitcher|31
Yankees|Pitcher|26
Yankees|Pitcher|21
Yankees|Not Pitcher|36
Yankees|Not Pitcher|25
Yankees|Not Pitcher|31

# Group By One Column and Get Mean, Min, and Max values by Group
First we'll group by `Team` with Pandas' `groupby` function. After grouping we can pass aggregation functions to the grouped object as a dictionary within the `agg` function. This dict takes the column that you're aggregating as a key, and either a single aggregation function or a list of aggregation functions as its value. To apply aggregations to multiple columns, just add additional key:value pairs to the dictionary.

```python
# group by Team, get mean, min, and max value of Age for each value of Team.
grouped_single = df.groupby('Team').agg({'Age': ['mean', 'min', 'max']})

print(grouped_single)
```

**Team**|**mean**|**min**|**max**
:-----:|:-----:|:-----:|:-----:
Red Sox|29.333333|22|40
Yankees|28.333333|21|36

Applying multiple aggregation functions to a single column will result in a [multiindex](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html#advanced-hierarchical). Working with multi-indexed columns is a pain and I'd recommend flattening this after aggregating by renaming the new columns.

You'll also see that your grouping column is now the dataframe's index. Reset your index to make this easier to work with later on.

```python
# rename columns
grouped_single.columns = ['age_mean', 'age_min', 'age_max']

# reset index to get grouped columns back
grouped_single = grouped_single.reset_index()

print(grouped_single)
```

**Team**|**age\_mean**|**age\_min**|**age\_max**
:-----:|:-----:|:-----:|:-----:
Red Sox|29.333333|22|40
Yankees|28.333333|21|36

# Grouping by Multiple Columns

It's simple to extend this to work with multiple grouping variables. Say you want to summarise player age by team AND position. You can do this by passing a list of column names to `groupby` instead of a single string value.

```python
grouped_multiple = df.groupby(['Team', 'Pos']).agg({'Age': ['mean', 'min', 'max']})
grouped_multiple.columns = ['age_mean', 'age_min', 'age_max']
grouped_multiple = grouped_multiple.reset_index()
print(grouped_multiple)
```

**Team**|**Pos**|**age\_mean**|**age\_min**|**age\_max**
:-----:|:-----:|:-----:|:-----:|:-----:
Red Sox|Not Pitcher|28.000000|22|33
Red Sox|Pitcher|30.666667|24|40
Yankees|Not Pitcher|30.666667|25|36
Yankees|Pitcher|26.000000|21|31



