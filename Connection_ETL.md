```python
import mysql.connector
import sqlite3
import pandas as pd
import html5lib
from matplotlib.dates import DateFormatter, date2num, WeekdayLocator, DayLocator, MONDAY
import datetime
import yfinance as yf
```

# Extracting Stock Data


```python
#Setting start and end dates
start = datetime.datetime(2010,6,29)
end = datetime.datetime(2022,10,15)
```


```python
Tesla = yf.download("TSLA", start, end)
Amazon = yf.download("AMZN", start, end)
```

    [*********************100%***********************]  1 of 1 completed
    [*********************100%***********************]  1 of 1 completed


# Setting Up Database Connection


```python
# import the module
import pymysql

from sqlalchemy import create_engine

# create sqlalchemy engine
engine = create_engine("mysql+pymysql://{user}:{password}@localhost/{database}"
                       .format(user = 'root',
                              password = 'Coors1998',
                              database = 'stocks'))
```


```python
#Reading data to sql
Amazon.to_sql('Amazon', con = engine, if_exists = 'append', chunksize = 1000)

```




    3097




```python
query = "SELECT * from Amazon"
```


```python
table = pd.read_sql(query , con = engine)
```


```python
table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-06-29</td>
      <td>5.813000</td>
      <td>5.824000</td>
      <td>5.300500</td>
      <td>5.430500</td>
      <td>5.430500</td>
      <td>257326000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-06-30</td>
      <td>5.429000</td>
      <td>5.634000</td>
      <td>5.405500</td>
      <td>5.463000</td>
      <td>5.463000</td>
      <td>194814000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-07-01</td>
      <td>5.445000</td>
      <td>5.584500</td>
      <td>5.335000</td>
      <td>5.548000</td>
      <td>5.548000</td>
      <td>170596000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-07-02</td>
      <td>5.546000</td>
      <td>5.564500</td>
      <td>5.428000</td>
      <td>5.457000</td>
      <td>5.457000</td>
      <td>89542000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-07-06</td>
      <td>5.532500</td>
      <td>5.626500</td>
      <td>5.450000</td>
      <td>5.503000</td>
      <td>5.503000</td>
      <td>104386000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>6189</th>
      <td>2022-10-10</td>
      <td>115.099998</td>
      <td>116.250000</td>
      <td>112.430000</td>
      <td>113.669998</td>
      <td>113.669998</td>
      <td>42339700</td>
    </tr>
    <tr>
      <th>6190</th>
      <td>2022-10-11</td>
      <td>112.709999</td>
      <td>115.480003</td>
      <td>110.389999</td>
      <td>112.209999</td>
      <td>112.209999</td>
      <td>56432200</td>
    </tr>
    <tr>
      <th>6191</th>
      <td>2022-10-12</td>
      <td>112.489998</td>
      <td>113.830002</td>
      <td>111.400002</td>
      <td>112.900002</td>
      <td>112.900002</td>
      <td>45728700</td>
    </tr>
    <tr>
      <th>6192</th>
      <td>2022-10-13</td>
      <td>107.879997</td>
      <td>113.440002</td>
      <td>105.349998</td>
      <td>112.529999</td>
      <td>112.529999</td>
      <td>86868100</td>
    </tr>
    <tr>
      <th>6193</th>
      <td>2022-10-14</td>
      <td>114.099998</td>
      <td>114.959999</td>
      <td>106.599998</td>
      <td>106.900002</td>
      <td>106.900002</td>
      <td>67737300</td>
    </tr>
  </tbody>
</table>
<p>6194 rows × 7 columns</p>
</div>




```python

```
