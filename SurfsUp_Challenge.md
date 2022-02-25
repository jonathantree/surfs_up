```python
# Dependencies
import numpy as np
import pandas as pd
%matplotlib inline
from matplotlib import style
style.use('fivethirtyeight')
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
from matplotlib.dates import DateFormatter

from datetime import datetime, timedelta


# Python SQL toolkit and Object Relational Mapper
import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy import inspect
from sqlalchemy.orm import Session
from sqlalchemy import create_engine, func
import datetime as dt
```


```python
engine = create_engine("sqlite:///hawaii.sqlite")

# reflect an existing database into a new model
Base = automap_base()
# reflect the tables
Base.prepare(engine, reflect=True)

# Save references to each table
Measurement = Base.classes.measurement
Station = Base.classes.station
```


```python
# Create our session (link) from Python to the DB
session = Session(engine)
```

## D1: Determine the Summary Statistics for June


```python
# 1. Import the sqlalchemy extract function.
from sqlalchemy import extract

# 2. Write a query that filters the Measurement table to retrieve the temperatures for the month of June. 
june_temps = []
june_temps = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date)==6).all()

```


```python
#  3. Convert the June temperatures to a list.
june_temps=list(june_temps)
```


```python
# 4. Create a DataFrame from the list of temperatures for the month of June. 
june_temps_df = pd.DataFrame(june_temps, columns=['date','temperature'])
```


```python
june_temps_df
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
      <th>date</th>
      <th>temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-06-01</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-06-02</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-06-03</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-06-04</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-06-05</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1695</th>
      <td>2017-06-26</td>
      <td>79.0</td>
    </tr>
    <tr>
      <th>1696</th>
      <td>2017-06-27</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>1697</th>
      <td>2017-06-28</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>1698</th>
      <td>2017-06-29</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>1699</th>
      <td>2017-06-30</td>
      <td>75.0</td>
    </tr>
  </tbody>
</table>
<p>1700 rows × 2 columns</p>
</div>




```python
# 5. Calculate and print out the summary statistics for the June temperature DataFrame.
june_temps_df.describe()
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
      <th>temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1700.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>74.944118</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.257417</td>
    </tr>
    <tr>
      <th>min</th>
      <td>64.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>73.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>75.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>77.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>85.000000</td>
    </tr>
  </tbody>
</table>
</div>



## D2: Determine the Summary Statistics for December


```python
# 6. Write a query that filters the Measurement table to retrieve the temperatures for the month of December.
dec_temps = []
dec_temps = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date)==12).all()
```


```python
# 7. Convert the December temperatures to a list.
dec_temps=list(dec_temps)
```


```python
# 8. Create a DataFrame from the list of temperatures for the month of December. 
dec_temps_df = pd.DataFrame(dec_temps, columns=['date','temperature'])
dec_temps_df
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
      <th>date</th>
      <th>temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-12-01</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-12-03</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-12-04</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-12-06</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-12-07</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1512</th>
      <td>2016-12-27</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>1513</th>
      <td>2016-12-28</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>1514</th>
      <td>2016-12-29</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>1515</th>
      <td>2016-12-30</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>1516</th>
      <td>2016-12-31</td>
      <td>65.0</td>
    </tr>
  </tbody>
</table>
<p>1517 rows × 2 columns</p>
</div>




```python
# 9. Calculate and print out the summary statistics for the Decemeber temperature DataFrame.
dec_temps_df.describe()
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
      <th>temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1517.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>71.041529</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.745920</td>
    </tr>
    <tr>
      <th>min</th>
      <td>56.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>69.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>71.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>74.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>83.000000</td>
    </tr>
  </tbody>
</table>
</div>



## Extra work


```python
inspector = inspect(engine)
inspector.get_table_names()
```




    ['measurement', 'station']




```python
# Get the column names for the table
column_names = inspector.get_columns('measurement')
for column_name in column_names:
    print(column_name["name"])
```

    id
    station
    date
    prcp
    tobs
    


```python
# Get the column names for the table
column_names = inspector.get_columns('station')
for column_name in column_names:
    print(column_name["name"])
```

    id
    station
    name
    latitude
    longitude
    elevation
    


```python
#Get precipiation data for the month of June, make a datafram and grab summary statistics
june_prcp = []
june_prcp = session.query(Measurement.date, Measurement.prcp).filter(extract('month', Measurement.date)==6).all()
june_prcp_df = pd.DataFrame(june_prcp, columns=['date','temperature'])
june_prcp_df.describe()
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
      <th>temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1574.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.136360</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.335731</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.020000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.120000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>4.430000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Get precipiation data for the month of December, make a datafram and grab summary statistics
dec_prcp = []
dec_prcp = session.query(Measurement.date, Measurement.prcp).filter(extract('month', Measurement.date)==12).all()
dec_prcp_df = pd.DataFrame(dec_prcp, columns=['date','temperature'])
dec_prcp_df.describe()
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
      <th>temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1405.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.216819</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.541399</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.030000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.150000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>6.420000</td>
    </tr>
  </tbody>
</table>
</div>



## Plots


```python
dec_temps_df.plot.hist(bins=10)
```




    <AxesSubplot:ylabel='Frequency'>




    
![png](SurfsUp_Challenge_files/SurfsUp_Challenge_21_1.png)
    



```python
dec_temps_df.set_index(dec_temps_df.date, inplace=True)
dec_temps_df.plot(rot=90, 
                  style=".",
                  ylabel = 'Temperature'
                  
                 )

```




    <AxesSubplot:xlabel='date', ylabel='Temperature'>




    
![png](SurfsUp_Challenge_files/SurfsUp_Challenge_22_1.png)
    



```python
dec_temps_df.reset_index(drop=True)
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
      <th>date</th>
      <th>temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-12-01</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-12-03</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-12-04</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-12-06</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-12-07</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1512</th>
      <td>2016-12-27</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>1513</th>
      <td>2016-12-28</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>1514</th>
      <td>2016-12-29</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>1515</th>
      <td>2016-12-30</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>1516</th>
      <td>2016-12-31</td>
      <td>65.0</td>
    </tr>
  </tbody>
</table>
<p>1517 rows × 2 columns</p>
</div>




```python
dec_temps_df.date = pd.Index(pd.to_datetime(dec_temps_df.date))
```


```python
mean_temps_dec = dec_temps_df.groupby(pd.Grouper(key='date', freq='1Y')).mean()
```


```python
mean_temps_dec.plot(style="x",
                  ylabel = 'Average Temperature'
)
```




    <AxesSubplot:xlabel='date', ylabel='Average Temperature'>




    
![png](SurfsUp_Challenge_files/SurfsUp_Challenge_26_1.png)
    



```python
dec_temps_df.dtypes
```




    date           datetime64[ns]
    temperature           float64
    dtype: object




```python
dec_temps_df.year = dec
# # date in MM-DD-YYYY format
# df['Birthday2'] = df['Birthday'].dt.strftime('%m-%d-%Y')
# # display the dataframe
# print(df)
```
