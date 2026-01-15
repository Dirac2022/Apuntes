
# Manipulating Time Series Data in Python


## Working with Time Series in Pandas


### How to use dates & times with pandas

In a **pandas** DataFrame any column can contain date or time information, but it is most important as a DataFrame index, because this converts the entire DataFrame into a time series.


<h5>Basic bluiding block: pd.Timestamp</h5>

Creating a Timestamp:

```python
import pandas as pd
from datetime import datetime
time_stamp = pd.Timestamp(datetime(2017, 1, 1))
pd.Timestamp('2017-01-01') == time_stamp
# True
```

```python
time_stamp
# Timestamp('2017-01-01 00:00:00')
```

`Timestamp` object has many attributes to store time-specific information

```python
time_stamp.year
# 2017
```

```python
time_stamp.day_name()
# 'Sunday'
```

<h5>pd.Period & freq</h5>
The period object always has a frequency, with months as the default.

```python
# Default: month-end
period = pd.Period('2017-01')
period
# Period('2017-01', 'M')
```

Period object has `freq` attribute to store frequency info

```python
# Convert to daily
period.asfreq('D')
# Period('2017-01-31', 'D')
```

Convert `pd.Period()` to `pd.Timestamp()` and back

```python
period.to_timestamp().to_period('M')
# Period('2017-01', 'M')
```

**You can also do basics date arithmetic

```python
period + 2
# Period('2017-03', 'M')
```


<h5>Sequences of dates & times</h5>
To  create a time series, you need a sequence of dates.

- `pd.date_range`: `start`, `end`, `periods`, `freq`

```python
# 'M' is deprecated for month, use 'ME' (MonthEnd)
index = pd.date_range(start='2017-1-1', periods=12, freq='ME')
index
```

Output:
```
DatetimeIndex(['2017-01-31', '2017-02-28', '2017-03-31', '2017-04-30',
               '2017-05-31', '2017-06-30', '2017-07-31', '2017-08-31',
               '2017-09-30', '2017-10-31', '2017-11-30', '2017-12-31'],
              dtype='datetime64[ns]', freq='ME')
```

A `pd.DateTimeIndex` is a sequence of Timestamp objects with frequency info

You can convert index to a `PeriodIndex`:

```python
index.to_period()
```

Output:
```
PeriodIndex(['2017-01', '2017-02', '2017-03', '2017-04', '2017-05', '2017-06',
             '2017-07', '2017-08', '2017-09', '2017-10', '2017-11', '2017-12'],
            dtype='period[M]')
```

> Now you can create a time series by setting the `DateTimeIndex` as the index of your Dataframe


**Create a time series: `pd.DateTimeIndex`**

```python
import numpy as np

data = np.random.random(size=(12,2)) # Random numbers: [0, 1]
df = pd.DataFrame(data=data, index=index)
df
```

Output:

|            | 0        | 1        |
| ---------- | -------- | -------- |
| 2017-01-31 | 0.006503 | 0.003620 |
| 2017-02-28 | 0.289295 | 0.205535 |
| 2017-03-31 | 0.828599 | 0.236781 |
| 2017-04-30 | 0.103812 | 0.913960 |
| 2017-05-31 | 0.717249 | 0.795678 |
| 2017-06-30 | 0.712788 | 0.687545 |
| 2017-07-31 | 0.638335 | 0.840795 |
| 2017-08-31 | 0.616654 | 0.663649 |
| 2017-09-30 | 0.697696 | 0.846846 |
| 2017-10-31 | 0.042861 | 0.164761 |
| 2017-11-30 | 0.276970 | 0.481666 |
| 2017-12-31 | 0.802296 | 0.403636 |


<h5>Frequency aliases & time info</h5>

| Period       | Alias |
| ------------ | ----- |
| Hour         | h     |
| Business day | B     |
| Calendar day | D     |
| Week         | W     |
| Month        | ME    |
| Quarter      | Q     |
| Year         | Y     |

**`pd.Timestamp()` attributes**

- `.second`, `.minute`, `.hour`
- `.day`, `.month`, `.quarter`, `.year`
- `.weekday`, `.dayofweek`, `.weekofyear`, `.dayofyear`




The default is daily frequency

### Indexing & resampling time series


### Lags, changes, and returns for stock prices series



## Basic Time Series Metrics & Resampling


## Window Functions: Rolling & Expanding Metrics


## Putting it all together: Building a value-weighted index



# Time Series Analysis in Python




# Visualizing Time Series Data in Python





# ARIMA Models in Python




# Machine Learning for Time Series Data in Python



