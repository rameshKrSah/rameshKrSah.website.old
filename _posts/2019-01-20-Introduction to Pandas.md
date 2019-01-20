---
title : "Introduction to Pandas"
date: 2019-01-20
mathjax: True
tags: [machine_learning]
---

# Introduction to Pandas

[pandas](pandas.pydata.org) is a column-oriented data analysis tool, which is used for handling and analyzing data. Many machine learning framework support pandas.

The primary data structure in *pandas* are implemented as two classes:
1. **DataFrame**,  is a table with rows and columns.
2. **Series**,  is a single column.

One way to create **Series** is by constructing a series object, like this:

```python
# Importing pandas and printing its version
import pandas as pd
print(pd.__version__)


# creating a series
print(pd.Series(['San Francisco', 'San Jose', 'Sacramento']))
```

    0.22.0
    0    San Francisco
    1         San Jose
    2       Sacramento
    dtype: object
    

**DataFrame** objects can be created by passing a dict mapping string column names to their respective **Series**. If the sereis don't match length, missing values are filled with special NAN values.


```python
city_names = pd.Series(['San Francisco', 'San Jose', 'Sacramento'])
population = pd.Series([852469, 145632, 680943])

pd.DataFrame({'City name' : city_names, 'Population' : population})

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
      <th>City name</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
    </tr>
  </tbody>
</table>
</div>



But most of the time, we load an entire file into a DataFrame. Here we load a file with California housing data from cloud.


```python
cali_hou_df = pd.read_csv("https://download.mlcc.google.com/mledu-datasets/california_housing_train.csv", sep=",")
cali_hou_df.describe()
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
      <th>longitude</th>
      <th>latitude</th>
      <th>housing_median_age</th>
      <th>total_rooms</th>
      <th>total_bedrooms</th>
      <th>population</th>
      <th>households</th>
      <th>median_income</th>
      <th>median_house_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>17000.000000</td>
      <td>17000.000000</td>
      <td>17000.000000</td>
      <td>17000.000000</td>
      <td>17000.000000</td>
      <td>17000.000000</td>
      <td>17000.000000</td>
      <td>17000.000000</td>
      <td>17000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-119.562108</td>
      <td>35.625225</td>
      <td>28.589353</td>
      <td>2643.664412</td>
      <td>539.410824</td>
      <td>1429.573941</td>
      <td>501.221941</td>
      <td>3.883578</td>
      <td>207300.912353</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2.005166</td>
      <td>2.137340</td>
      <td>12.586937</td>
      <td>2179.947071</td>
      <td>421.499452</td>
      <td>1147.852959</td>
      <td>384.520841</td>
      <td>1.908157</td>
      <td>115983.764387</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-124.350000</td>
      <td>32.540000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>1.000000</td>
      <td>0.499900</td>
      <td>14999.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-121.790000</td>
      <td>33.930000</td>
      <td>18.000000</td>
      <td>1462.000000</td>
      <td>297.000000</td>
      <td>790.000000</td>
      <td>282.000000</td>
      <td>2.566375</td>
      <td>119400.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-118.490000</td>
      <td>34.250000</td>
      <td>29.000000</td>
      <td>2127.000000</td>
      <td>434.000000</td>
      <td>1167.000000</td>
      <td>409.000000</td>
      <td>3.544600</td>
      <td>180400.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-118.000000</td>
      <td>37.720000</td>
      <td>37.000000</td>
      <td>3151.250000</td>
      <td>648.250000</td>
      <td>1721.000000</td>
      <td>605.250000</td>
      <td>4.767000</td>
      <td>265000.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>-114.310000</td>
      <td>41.950000</td>
      <td>52.000000</td>
      <td>37937.000000</td>
      <td>6445.000000</td>
      <td>35682.000000</td>
      <td>6082.000000</td>
      <td>15.000100</td>
      <td>500001.000000</td>
    </tr>
  </tbody>
</table>
</div>



The example above used DataFrame.describe to show intresting statistics about a DataFrame. Another useful function is DataFrame.head, which shows the first few records of a DataFrame.


```python
cali_hou_df.head()
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
      <th>longitude</th>
      <th>latitude</th>
      <th>housing_median_age</th>
      <th>total_rooms</th>
      <th>total_bedrooms</th>
      <th>population</th>
      <th>households</th>
      <th>median_income</th>
      <th>median_house_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-114.31</td>
      <td>34.19</td>
      <td>15.0</td>
      <td>5612.0</td>
      <td>1283.0</td>
      <td>1015.0</td>
      <td>472.0</td>
      <td>1.4936</td>
      <td>66900.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-114.47</td>
      <td>34.40</td>
      <td>19.0</td>
      <td>7650.0</td>
      <td>1901.0</td>
      <td>1129.0</td>
      <td>463.0</td>
      <td>1.8200</td>
      <td>80100.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-114.56</td>
      <td>33.69</td>
      <td>17.0</td>
      <td>720.0</td>
      <td>174.0</td>
      <td>333.0</td>
      <td>117.0</td>
      <td>1.6509</td>
      <td>85700.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-114.57</td>
      <td>33.64</td>
      <td>14.0</td>
      <td>1501.0</td>
      <td>337.0</td>
      <td>515.0</td>
      <td>226.0</td>
      <td>3.1917</td>
      <td>73400.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-114.57</td>
      <td>33.57</td>
      <td>20.0</td>
      <td>1454.0</td>
      <td>326.0</td>
      <td>624.0</td>
      <td>262.0</td>
      <td>1.9250</td>
      <td>65500.0</td>
    </tr>
  </tbody>
</table>
</div>



Another powerful feature of *pandas* is graphing. For example, DataFrame.hist lets us quickly study the distribution of values in a column.



```python
cali_hou_df.hist('housing_median_age')
```

    array([[<matplotlib.axes._subplots.AxesSubplot object at 0x7f7351b13828>]],
          dtype=object)



![png](../assets/images/Introduction%20to%20Pandas_10_1.png)


We can access DataFrame data using Python dict/list operations:


```python
cities = pd.DataFrame({ 'City name': city_names, 'Population': population })
print(type(cities['City name']))
cities['City name']
```

    <class 'pandas.core.series.Series'>
    
    0    San Francisco
    1         San Jose
    2       Sacramento
    Name: City name, dtype: object




```python
print(type(cities['City name'][1]))
cities['City name'][1]
```

    <class 'str'>
    'San Jose'




```python
print(type(cities[0:2]))
cities[0:2]
```

    <class 'pandas.core.frame.DataFrame'>
    

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
      <th>City name</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
    </tr>
  </tbody>
</table>
</div>



We can apply Python's basic arithmetic operation to Series.


```python
population / 1000
```

    0    852.469
    1    145.632
    2    680.943
    dtype: float64




```python
cities
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
      <td>21</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(cities[['Population', 'Area']]) # read the columns for Population and Area
```

       Population  Area
    0      852469    45
    1      145632   212
    2      680943    21
    


```python
cities[cities['Population'] > 150000]
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
      <td>21</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
cities[:2] # Get the firs two rows
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
cities.loc[[0], ['Area', 'Population Density']] # selects the subset of the dataframe by specifying the rows and columns
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
      <th>Area</th>
      <th>Population Density</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>45</td>
      <td>18943.755556</td>
    </tr>
  </tbody>
</table>
</div>



[NumPy](numpy.org) is a popular toolkit for scientific computing. *pandas* Series can be used as arguments to most Numpy functions.


```python
import numpy as np
np.log(population)
```




    0    13.655892
    1    11.888838
    2    13.431234
    dtype: float64



For more complex single-column transformation, we can use `Series.apply`. Like the Python map function, `Series.apply` accepts as an argument a lambda function, which is applied to each value.


```python
population.apply(lambda val: val > 1000000)
```

    0    False
    1    False
    2    False
    dtype: bool



Modifying DataFrames is also straightforward.


```python
cities['Area'] = pd.Series([45, 212, 21])
cities['Population Density'] = cities['Population'] / cities['Area']
cities
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
      <td>21</td>
      <td>32425.857143</td>
    </tr>
  </tbody>
</table>
</div>




```python
cities['Is large and has a Saint'] = (cities['Area'] > 50) & cities['City name'].apply(lambda name: name.startswith('San'))
cities
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
      <td>21</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



Both Series and DataFrame objects also define an index property that assigns an identifier value to each Series item or DataFrame row. By default, at construction, *pandas* assigns index values that reflect  ordering of the source data. Once created, the index values are stable; that is, they do no change when data is reordered.


```python
city_names.index
```

    RangeIndex(start=0, stop=3, step=1)




```python
cities.index
```

    RangeIndex(start=0, stop=3, step=1)



Call DataFrame.reindex to manually reorder the rows.


```python
cities.reindex([2, 0, 1])
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
      <td>21</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



Reindexing is a great way to shuffle (randomize) a DataFrame.


```python
cities.reindex(np.random.permutation(cities.index))
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
      <td>21</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
cities.reindex([1, 2, 3])
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632.0</td>
      <td>212.0</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943.0</td>
      <td>21.0</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



If our reindex input array includes values not in the original DataFrame index values, reindex will add rows for these "missing" indices and populate all corresponding columns with NaN values. This behaviour is desirable because indexes are often strings pulled from the actual data, and allowing missing indices makes it easy to reindex using an external list, as we don't have to worry about sanitizing the input.

We can use the drop method to remove rows and columns from the dataframe. With axis value set to 0 we will drop the row and axis value set to 1 will drop the columns. By default the axis value is set to 0.


```python
cities
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>680943</td>
      <td>21</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
cities.drop([2]) # drop the third row from the data frame
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
      <th>City name</th>
      <th>Population</th>
      <th>Area</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>852469</td>
      <td>45</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>145632</td>
      <td>212</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
cities.drop(['Area', 'Population'], axis = 1) # drop the coulumns of Area and Population
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
      <th>City name</th>
      <th>Population Density</th>
      <th>Is large and has a Saint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Francisco</td>
      <td>18943.755556</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Jose</td>
      <td>686.943396</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sacramento</td>
      <td>32425.857143</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



# References
- [Google Getting Started with Pandas](https://colab.research.google.com/notebooks/mlcc/intro_to_pandas.ipynb)
