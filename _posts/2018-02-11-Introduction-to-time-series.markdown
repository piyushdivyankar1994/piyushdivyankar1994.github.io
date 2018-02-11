---
layout: post
title: "Introduction to Time Series."
date: 2018-02-11 09:00:00 +0530
---

# Introduction to Time Series

First things first let's define what is a time series.

> **Time Series** is a list of data points that are indexed by time.

This is a simple definition that will serve our purposes for some time. Let's see some examples of time series data. Since I want this blog to be centered around finance let's take stock prices as an example.

## Getting stock data

To get stock data we use [pandas-datareader](https://pandas-datareader.readthedocs.io/en/latest/). We will fetch the close price of NIFTY-50 for the past year. We are querying data from quandl.


```python
import pandas as pd
import pandas_datareader.data as web
import datetime

# Specify start and end date.
start = datetime.datetime(2017, 1, 1)
end   = datetime.datetime(2018, 1, 1)

nifty = web.DataReader('NSE/NIFTY_50', 'quandl', start, end)

# First 5 rows for NIFTY_50 data
print(nifty.head())
```

                    Open      High       Low     Close  SharesTraded  TurnoverRsCr
    Date
    2018-01-01  10531.70  10537.85  10423.10  10435.55   134532090.0       7546.56
    2017-12-29  10492.35  10538.70  10488.65  10530.70   156736221.0       8943.10
    2017-12-26  10512.30  10545.45  10477.95  10531.50   160417384.0       9043.77
    2017-12-22  10457.30  10501.10  10448.25  10493.00   143119167.0       8755.32
    2017-12-21  10473.95  10473.95  10426.90  10440.30   156646972.0       9411.20


As you are able to see we have the data for the first 5 entries of the NIFTY_50 index. See that index of the data is dates.

## Visualiztion
The first thing we want to do with a time series is plot it. We want to have a line plot where x-axis is time and the y-axis is the variable. Let's plot close prices of the index.


```python
import matplotlib.pyplot as plt

df = nifty['Close']
df.plot(figsize=(15,8))
plt.ylabel('NIFTY-50')
plt.show()
```


![nifty50plot]({{"/assets/img/Introduction_5_0.png"}})


Visualization is the first step in the time series analysis. It tells us many things about the data.

**What does the above plot tell us about close prices of Nifty-50?**
1. There is a general upward trend to the close price.
2. There is some fluctuation but it isn't that noisy.
3. There seems to be some gradual increase and a quicker fall happening periodicallys.

These are observations in layman's terms in future we will see how to improve upon these by using some specific terminology.
