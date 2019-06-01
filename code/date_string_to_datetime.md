---
layout: archive
title: "Turn Date Strings into Datetime Objects"
permalink: /code/date_string_to_datetime
author_profile: true
date: 2019-06-01
redirect_from:
  - /datetime
---

{% include base_path %}

This post shows how to properly format a date string and turn it into a datetime object using Pandas' `pd.to_datetime` function.

# Background

Date values in raw data will usually be read into a dataframe as a string type. To use these values for date math or perform any sort of timeseries analysis, these will need to be converted into a proper datetime format that Python understands. There are a few ways to turn date strings into datetimes. Pandas' `to_datetime` funtion is one fairly easy way to do it.

# Imports
```python
import pandas as pd
```

# Create Some Example Date Strings
```python
datetimes = ['2018-10-19 23:28:40.798061', '2018-10-18 11:10:44.453098', '2018-10-20 01:10:01.759478']
dates = ['2018-01-01', '2018-04-22', '2018-09-09']
more_dates = ['August 1, 2018', 'January 10, 2016', 'September 26, 1988']
```

Most of the time, `pd.to_datetime` will be able to infer the correct date format without any help. If it's unable to do this, you will need to specify the datestring's format. [strftime.org](http://strftime.org/) is a good point of reference for creating strftime format. I've also had some luck using [strftimer.com](http://strftimer.com/) as a starting point, where you can paste in a date and the site returns its strftime format. The value reaturned is based on Ruby's format, but it's about the same as Python's.

It's useful to start with the default setting of `errors='raise'`, so that you're aware of any deviations from the expected format. If there are a few rogue values that can't be fixed, `errors='coerce'` will coerce these entries to NaTs.

```python
pd.to_datetime(datetimes, format='%Y-%m-%d %H:%M:%S.%f', errors='coerce')
pd.to_datetime(dates, format='%Y-%m-%d', errors='coerce')
pd.to_datetime(more_dates, format='%B %d, %Y', errors='coerce')
```

`DatetimeIndex(['2018-10-19 23:28:40.798061', '2018-10-18 11:10:44.453098',
               '2018-10-20 01:10:01.759478'],
              dtype='datetime64[ns]', freq=None)`

`DatetimeIndex(['2018-01-01', '2018-04-22', '2018-09-09'], dtype='datetime64[ns]', freq=None)`

`DatetimeIndex(['2018-08-01', '2016-01-10', '1988-09-26'], dtype='datetime64[ns]', freq=None)`