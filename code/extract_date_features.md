---
layout: archive
title: "Extract Month, Year and Day from a Date"
permalink: /code/extract_date_features
author_profile: true
redirect_from:
  - /get_month_year
---

{% include base_path %}

Date strings aren't very useful in their raw form, but extracting numeric features such as a date's Month, Year, and Day can help to represent seasonality in your data. This post shows how extract Month and Year from a date string.

# Imports
```python
import pandas as pd
```

# Create Some Example Data
```python
data = {'date': ['2016-01-01', '2018-03-02', '2017-04-16', '2018-01-04', '2016-02-11', '2018-02-12']}
df = pd.DataFrame(data)
```

First, make sure the date column is of type `datetime`. See [here](/code/date_string_to_datetime) for more detail on this. Then, extract Month, Year, and Day by calling `dt.month`, `dt.year`, and `dt.day` on the `datetime` column.

```python
df['date'] = pd.to_datetime(df['date'])
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
print(df)
```

|**date**|**month**|**year**|**day**
:-----:|:-----:|:-----:|:-----:|
2016-01-01|2016|1|1
2018-03-02|2018|3|2
2017-04-16|2017|4|16
2018-01-04|2018|1|4
2016-02-11|2016|2|11
2018-02-12|2018|2|12

And that's it! Easy enough.