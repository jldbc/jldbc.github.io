---
layout: archive
title: "Get the Difference Between Two Dates"
permalink: /code/date_differences
author_profile: true
date: 2019-06-01
last_modified_at: 2019-06-01
redirect_from:
  - /date_math
---

{% include base_path %}

Simple date math can create useful features for machine learning models and analyses alike. This post shows how to get the number of days between two dates. 

# Imports
```python
import pandas as pd
```

# Create Some Example Data

Say we have a dataset of ad campaigns. Each campaign has a start date, and one row for each day the campaign was live. 
```python
data = {'campaign_id': [123, 123, 123, 123, 124, 124],
		'campaign_start_date': ['2018-01-01', '2018-01-01', '2018-01-01', '2018-01-01', '2018-02-11', '2018-02-11'],
		'date': ['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04', '2018-02-11', '2018-02-12'],
		'impressions': [1000, 1113, 1755, 3511, 412, 988]}
df = pd.DataFrame(data)
print(df)
```

|**campaign\_id**|**campaign\_start\_date**|**date**|**impressions**
:-----:|:-----:|:-----:|:-----:
123|2018-01-01|2018-01-01|1000
123|2018-01-01|2018-01-02|1113
123|2018-01-01|2018-01-03|1755
123|2018-01-01|2018-01-04|3511
124|2018-02-11|2018-02-11|412
124|2018-02-11|2018-02-12|988

To work with this type of data, you may want to know how many days it's been since the campaign first went live at each point in time (`date` - `campaign_start_date`). Subtracting two columns of type string will raise an error, so there are some additional steps to follow to get the difference between two date columns.

First, make sure the two date columns are of type `datetime`. See [here](/code/date_string_to_datetime) for more detail on this. 

```python
df['campaign_start_date'] = pd.to_datetime(df['campaign_start_date'])
df['date'] = pd.to_datetime(df['date'])
```

With the two columns as type `datetime`, you can now subtract them. To get the subtracted value in a usable numeric format, you will need to specify its unit of time as being in days with `dt.days`. 
```python
df['days_since_start'] = (df['date'] - df['campaign_start_date']).dt.days
print(df)
```

|**campaign\_id**|**campaign\_start\_date**|**date**|**impressions**|**days\_since\_start**
:-----:|:-----:|:-----:|:-----:|:-----:
123|2018-01-01|2018-01-01|1000|0
123|2018-01-01|2018-01-02|1113|1
123|2018-01-01|2018-01-03|1755|2
123|2018-01-01|2018-01-04|3511|3
124|2018-02-11|2018-02-11|412|0
124|2018-02-11|2018-02-12|988|1


As there's no common definition for the number of days in a month or year, there's no option to specify `dt.months` or `dt.years`. You can approximate this, however, by dividing the output by 30 or 365.
