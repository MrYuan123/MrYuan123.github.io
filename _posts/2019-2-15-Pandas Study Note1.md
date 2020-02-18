---
layout:     post
title:      "Pandas Study Note1"
subtitle:   " \"Hello World, Hello Blog\""
date:       2019-2-15 14:00
author:     "Leonard Yuan"
header-img: "img/post-bg-miui6.jpg"
catalog: true
tags:
    - Data Science
    - Pandas
    
---

# Pandas Study Note

## 1. About Anaconda
Anaconda is a high efficient Python platform, I just want to notice one of hte important issue: how to manage library.


- list all libraries


```python
conda list
```

- install library


```python
conda install xxx
```

- Update all libraries


```python
conda update --all 
```

## 2. Pandas Data Structure

Pandas has highe level data structures and functions than Numpy. Actually, Pandas is built on the top of Numpy. The primary data object of Pandas is **DataFrame** and **Series**.

### a. Series

Series is like one demensional array, we can it like this:


```python
from pandas import Series, DataFrame
import pandas as pd
import numpy as np
obj = Series([2,3,5,6,7])
```


```python
obj
obj.index
obj.values
```




    array([2, 3, 5, 6, 7])



Also, you can set index for your Series, like:


```python
obj = Series([2,3,4,5,6,7], index=['a','b','c','m','r','t'])
```


```python
obj
```




    a    2
    b    3
    c    4
    m    5
    r    6
    t    7
    dtype: int64




```python
obj['a']
```




    2



You can calculate on the Series directly, like blew:


```python
obj[obj >5] # Get data which value is beyond 5
```




    r    6
    t    7
    dtype: int64



Also, sometimes we can use **dictionary** to build Series, like:


```python
test = {'a':12, 'b':234,'c':23}
obj3 = Series(test)
```


```python
obj3
```




    a     12
    b    234
    c     23
    dtype: int64



Series can also be operated directly. In other words, Series can make calculation.


```python
dict1 = {'a':21,'b':23,'c':23,'e':13}
dict2 = {'a':23,'b':22,'e':10}
Series(dict1) + Series(dict2)
```




    a    44.0
    b    45.0
    c     NaN
    e    23.0
    dtype: float64



### b. DataFrame

DataFrame is a kind of data structure in **Pandas**, which is similar with data table. 


```python
data = {'state':['ohio','Mass','CA','Nevada'],
        'year':[1990,1890,1920,1934],
        'pop':[1.2,3.4,4.5,6.7]
       }
frame = DataFrame(data)
frame
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
      <th>state</th>
      <th>year</th>
      <th>pop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ohio</td>
      <td>1990</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mass</td>
      <td>1890</td>
      <td>3.4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CA</td>
      <td>1920</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Nevada</td>
      <td>1934</td>
      <td>6.7</td>
    </tr>
  </tbody>
</table>
</div>



Or, we can decide the sequence of the columns, like:


```python
frame2 = DataFrame(data, columns=['state','pop','year'])
frame2
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
      <th>state</th>
      <th>pop</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ohio</td>
      <td>1.2</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934</td>
    </tr>
  </tbody>
</table>
</div>



If you want to set index, you can also operate like below:


```python
frame3 = DataFrame(data,  columns=['state','pop','year','status'], index=['one','two','three','four'])
frame3
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
      <th>state</th>
      <th>pop</th>
      <th>year</th>
      <th>status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>ohio</td>
      <td>1.2</td>
      <td>1990</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>three</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame3['pop']
```




    one      1.2
    two      3.4
    three    4.5
    four     6.7
    Name: pop, dtype: float64




```python
frame3['state']['four']
```




    'Nevada'



You can set value for entire column, like:


```python
frame3['status'] = 'Pending'
frame3
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
      <th>state</th>
      <th>pop</th>
      <th>year</th>
      <th>status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>ohio</td>
      <td>1.2</td>
      <td>1990</td>
      <td>Pending</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890</td>
      <td>Pending</td>
    </tr>
    <tr>
      <th>three</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920</td>
      <td>Pending</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934</td>
      <td>Pending</td>
    </tr>
  </tbody>
</table>
</div>



Sometimes, you want to set value to some positions of a column, you can **Series** to achieve that, like:


```python
statusC = Series(['good','bad'], index = ['one', 'three'])
frame3['status'] = statusC
frame3
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
      <th>state</th>
      <th>pop</th>
      <th>year</th>
      <th>status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>ohio</td>
      <td>1.2</td>
      <td>1990</td>
      <td>good</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>three</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920</td>
      <td>bad</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



If you want to delete certain column, you can **del** to achieve that, like:


```python
del frame3['status']
frame3
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
      <th>state</th>
      <th>pop</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>ohio</td>
      <td>1.2</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890</td>
    </tr>
    <tr>
      <th>three</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934</td>
    </tr>
  </tbody>
</table>
</div>



We can get the transposition of a table, like:


```python
frame3.T
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>state</th>
      <td>ohio</td>
      <td>Mass</td>
      <td>CA</td>
      <td>Nevada</td>
    </tr>
    <tr>
      <th>pop</th>
      <td>1.2</td>
      <td>3.4</td>
      <td>4.5</td>
      <td>6.7</td>
    </tr>
    <tr>
      <th>year</th>
      <td>1990</td>
      <td>1890</td>
      <td>1920</td>
      <td>1934</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame3
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
      <th>state</th>
      <th>pop</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>ohio</td>
      <td>1.2</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890</td>
    </tr>
    <tr>
      <th>three</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934</td>
    </tr>
  </tbody>
</table>
</div>



In Pandas, you can use index to add a row, like:


```python
DataFrame(frame3, index = ['two','three','four','five'])
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
      <th>state</th>
      <th>pop</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>two</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



We can set the names of the columns and index, like: 


```python
frame3.index.name = 'Number'
frame3.columns.name = 'Column'
frame3
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
      <th>Column</th>
      <th>state</th>
      <th>pop</th>
      <th>year</th>
    </tr>
    <tr>
      <th>Number</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>ohio</td>
      <td>1.2</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Mass</td>
      <td>3.4</td>
      <td>1890</td>
    </tr>
    <tr>
      <th>three</th>
      <td>CA</td>
      <td>4.5</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Nevada</td>
      <td>6.7</td>
      <td>1934</td>
    </tr>
  </tbody>
</table>
</div>



When we want to get the values of the DataFrame, we can operate like this:


```python
frame3.values
```




    array([['ohio', 1.2, 1990],
           ['Mass', 3.4, 1890],
           ['CA', 4.5, 1920],
           ['Nevada', 6.7, 1934]], dtype=object)



### c.Index Object

This is another one useful data structure of **Pandas**, we can use this to convert the tags of Series or DataFrame into a **Index**, like below:


```python
newobj = Series(range(4), index = ['a','b','c','d'])
index = newobj.index
index
```




    Index(['a', 'b', 'c', 'd'], dtype='object')



**Note: Index is static, so it cannot be reassigned any new value.**

By using Index, different data sets can share same Index, like:


```python
newobj2 = Series(range(2,6), index = index)
newobj2
```




    a    2
    b    3
    c    4
    d    5
    dtype: int64



Sometimes, when we want to find whether some variables in columns or index, we can do it like this:


```python
'state' in frame3.columns
```




    True




```python
'five' in frame3.index
```




    False



There are some functions on Index.

|   Number  |    Method  |Attribute | 
|----------|:-------------:|------:|
|1|append|Connect another Index into a new Index |
|2|diff|Get the difference set of two Indexs|
|3|intersection|Get the union set of two Indexs|
|4|delete(i)| Delete key of position i, getting a new Index|
|5|is_unique|When index do not repeat, return True|

## 3. Basic Functions

### a. reindex

This function can be used to reindex the Series, and return a new data set, like:


```python
obj = Series([1,2,3,4], index = ['a','b','c','d'])
obj
```




    a    1
    b    2
    c    3
    d    4
    dtype: int64




```python
obj.reindex(['b','c','e','a','d'])
```




    b    2.0
    c    3.0
    e    NaN
    a    1.0
    d    4.0
    dtype: float64



We can there is a value NAN because of a new index, and we can set a default value in function **reindex**, so panadas can set a default value in empty place, like:


```python
obj.reindex(['b','c','e','a','d'], fill_value=0)
```




    b    0
    c    0
    e    0
    a    0
    d    0
    dtype: int64



Sometimes, we should take insert operation on **Series**, we can also use **reindex** to achieve that, like: s


```python
obj3 = Series(['blue','purple','yellow'], index = [0,2,4])
obj3
```




    0      blue
    2    purple
    4    yellow
    dtype: object




```python
obj3.reindex(range(6), method='ffill')
```




    0      blue
    1      blue
    2    purple
    3    purple
    4    yellow
    5    yellow
    dtype: object



There are two ways to fill empty places: 

- **ffill/pad**

- **bfill/backfill**

For **DataFrame**, we can also use reindex to change the sequence of columns, indexs and empty places.

First of all, we can create a DataFrame object, it is about states datas, like:


```python
stateframe = DataFrame(np.arange(9).reshape(3,3), index = ['a','b','c'], columns =['Ohio','Texas', 'California'])
stateframe
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
      <th>Ohio</th>
      <th>Texas</th>
      <th>California</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>b</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>6</td>
      <td>7</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
stateframe2 = stateframe.reindex(columns = ['Ohio','Texas', 'Mass','California'])
stateframe2
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
      <th>Ohio</th>
      <th>Texas</th>
      <th>Mass</th>
      <th>California</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>1</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>b</th>
      <td>3</td>
      <td>4</td>
      <td>NaN</td>
      <td>5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>6</td>
      <td>7</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
stateframe2 = stateframe2.reindex(index = ['a','b','c','d'], method = 'ffill', columns = ['Ohio','Texas', 'Mass','California'])
stateframe2
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
      <th>Ohio</th>
      <th>Texas</th>
      <th>Mass</th>
      <th>California</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>1</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>b</th>
      <td>3</td>
      <td>4</td>
      <td>NaN</td>
      <td>5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>6</td>
      <td>7</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
    <tr>
      <th>d</th>
      <td>6</td>
      <td>7</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



If we think using **reindex** is over complicated, we can use **ix** ro achieve reindex operation, like:


```python
stateframe2.ix[['a','c','b','d'],['Ohio','Texas', 'Mass','California']]
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:1: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      """Entry point for launching an IPython kernel.





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
      <th>Ohio</th>
      <th>Texas</th>
      <th>Mass</th>
      <th>California</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>1</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>6</td>
      <td>7</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
    <tr>
      <th>b</th>
      <td>3</td>
      <td>4</td>
      <td>NaN</td>
      <td>5</td>
    </tr>
    <tr>
      <th>d</th>
      <td>6</td>
      <td>7</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



### b. Drop Data

When we want to delete some datas from data set, we can use function: **drop( )**.


```python
data = DataFrame(np.arange(16).reshape(4,4), index = ['ohio','CA','MA','NYC'], columns = ['one','two','three','four'])
data
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>CA</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.drop('ohio')
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.drop(['CA','NYC'])
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



If you want to delete a column from a data table, you should use **"axis = 1"** to sign that you will delete along column.


```python
data.drop(['one'], axis = 1)
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
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>CA</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.drop(['one','two'], axis = 1)
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
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>CA</th>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



### c.  Indexes, Selection and Filter

The mechanism of **Series** Indexes is similar to **Numpy** Indexes, but the indexes of Series is not limited as Integer type.I will show as below:


```python
obj = Series(np.arange(4), index = ['a','b','c','d'])
obj
```




    a    0
    b    1
    c    2
    d    3
    dtype: int64




```python
obj[0:4]
```




    a    0
    b    1
    c    2
    d    3
    dtype: int64




```python
obj[obj<2]
```




    a    0
    b    1
    dtype: int64




```python
data
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>CA</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
data['one']
```




    ohio     0
    CA       4
    MA       8
    NYC     12
    Name: one, dtype: int64




```python
data.T['CA']
```




    one      4
    two      5
    three    6
    four     7
    Name: CA, dtype: int64



We can also use slice operation on DataFrame, like:


```python
data[:-2]
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>CA</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



We can use condition judgement on **DataFrame**, then we can get the datas which match the requirement, like:


```python
data[data['three'] > 6]
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>MA</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



We can take operation on all position which matches the requirement, like:


```python
data[data > 5] =0
data
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>CA</th>
      <td>4</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
data = DataFrame(np.arange(16).reshape(4,4), index = ['ohio','CA','MA','NYC'], columns = ['one','two','three','four'])
data
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
      <th>one</th>
      <th>two</th>
      <th>three</th>
      <th>four</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>CA</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



You can also use **ix[  ]** to acquire datas from data set, like:


```python
data.ix['ohio', ['one','two']]
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:1: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      """Entry point for launching an IPython kernel.





    one    0
    two    1
    Name: ohio, dtype: int64




```python
data.ix[3]
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:1: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      """Entry point for launching an IPython kernel.





    one      12
    two      13
    three    14
    four     15
    Name: NYC, dtype: int64




```python
data.ix[data.three > 6, :3]
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:1: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      """Entry point for launching an IPython kernel.





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
      <th>one</th>
      <th>two</th>
      <th>three</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>MA</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>NYC</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>



## 4. Arithmetic Operation and Alignment of Data

In Pandas, we can take arithmetic operation directly on objects, we can show as below:


```python
s1 = Series(range(5), index = ['a','b','c','d','e'])
s2 = Series(range(6), index = ['b','d','e','c','m','f'])
s1+ s2
```




    a    NaN
    b    1.0
    c    5.0
    d    4.0
    e    6.0
    f    NaN
    m    NaN
    dtype: float64



For those no overlapping index, Pandas will use to **NAN** to fill those places.

Toward DataFrame, we can also take arithmetic operation on different DataFrames, like:


```python
df1 = DataFrame(np.arange(9).reshape(3,3), columns = list('abc'), index = ['CA','MA','TS'])
df2 = DataFrame(np.arange(12).reshape(4,3), columns = list('bce'), index = ['CA','MA','TS', 'OH'])
df1 + df2
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>NaN</td>
      <td>7.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>OH</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TS</th>
      <td>NaN</td>
      <td>13.0</td>
      <td>15.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



We can see that, for the empty places, Pandas will fill **NAN** in that, but sometimes, we should set certain default number on that, like:


```python
df1.add(df2, fill_value = 0)
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>0.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>3.0</td>
      <td>7.0</td>
      <td>9.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>OH</th>
      <td>NaN</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>TS</th>
      <td>6.0</td>
      <td>13.0</td>
      <td>15.0</td>
      <td>8.0</td>
    </tr>
  </tbody>
</table>
</div>



Here are four different functions on arithmetic operations:

- **add( )**

- **sub( )**

- **div( )**

- **mul( )**


```python
df1.mul(df2, fill_value = 1)
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>3.0</td>
      <td>12.0</td>
      <td>20.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>OH</th>
      <td>NaN</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>TS</th>
      <td>6.0</td>
      <td>42.0</td>
      <td>56.0</td>
      <td>8.0</td>
    </tr>
  </tbody>
</table>
</div>



### a.  Calculation Between DataFrame and Series

In Pandas library, we can take calculation between **DataFrame** and **Series**, like:


```python
df3 = DataFrame(np.arange(12).reshape(4,3), columns = list('bce'), index = ['CA','MA','TS', 'OH'])
df3
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
      <th>b</th>
      <th>c</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>TS</th>
      <td>6</td>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>OH</th>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
newframe = df3.ix[0]
newframe
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:1: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      """Entry point for launching an IPython kernel.





    b    0
    c    1
    e    2
    Name: CA, dtype: int64




```python
df3 - newframe
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
      <th>b</th>
      <th>c</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>TS</th>
      <td>6</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>OH</th>
      <td>9</td>
      <td>9</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
series = df3['b']
series
```




    CA    0
    MA    3
    TS    6
    OH    9
    Name: b, dtype: int64




```python
df3.sub(series, axis = 0)
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
      <th>b</th>
      <th>c</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>TS</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>OH</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



## 5. Function  Application and Mapping

First of all, we should build a data object, like:


```python
frame = DataFrame(np.random.randn(4, 3), columns = list('bde'), index = ['Utah', 'Ohio','Texas', 'Oregon'])
```


```python
frame
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
      <th>b</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Utah</th>
      <td>1.434118</td>
      <td>-0.820673</td>
      <td>0.610912</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>0.572641</td>
      <td>0.054709</td>
      <td>-0.257323</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>-2.293399</td>
      <td>-0.407289</td>
      <td>1.037199</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>-0.430910</td>
      <td>-1.018978</td>
      <td>-1.231238</td>
    </tr>
  </tbody>
</table>
</div>




```python
np.abs(frame)
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
      <th>b</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Utah</th>
      <td>1.434118</td>
      <td>0.820673</td>
      <td>0.610912</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>0.572641</td>
      <td>0.054709</td>
      <td>0.257323</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>2.293399</td>
      <td>0.407289</td>
      <td>1.037199</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>0.430910</td>
      <td>1.018978</td>
      <td>1.231238</td>
    </tr>
  </tbody>
</table>
</div>



If we want to apply a function on a entire column or row, we can use function **apply( )** to achieve, like:


```python
f = lambda x: x.max() - x.min()
```


```python
frame.apply(f)
```




    b    3.727518
    d    1.073687
    e    2.268437
    dtype: float64




```python
frame.apply(f, axis = 1)
```




    Utah      2.254791
    Ohio      0.829963
    Texas     3.330598
    Oregon    0.800329
    dtype: float64



We can also use function to return a **Series**, which contains muti-values:


```python
def f(x):
    return Series([x.max(),x.min()], index = ['max', 'min'])
frame.apply(f)
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
      <th>b</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>max</th>
      <td>1.434118</td>
      <td>0.054709</td>
      <td>1.037199</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-2.293399</td>
      <td>-1.018978</td>
      <td>-1.231238</td>
    </tr>
  </tbody>
</table>
</div>



If we want to operate all of elements in DataFrame, we can use function **applymap** to achieve that, like:


```python
format = lambda x: '%.2f'% x
```


```python
frame.applymap(format)
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
      <th>b</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Utah</th>
      <td>1.43</td>
      <td>-0.82</td>
      <td>0.61</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>0.57</td>
      <td>0.05</td>
      <td>-0.26</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>-2.29</td>
      <td>-0.41</td>
      <td>1.04</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>-0.43</td>
      <td>-1.02</td>
      <td>-1.23</td>
    </tr>
  </tbody>
</table>
</div>



There is a similar function in Series , we can also use that to operate data in a function, like:


```python
frame['b'].map(format)
```




    Utah       1.43
    Ohio       0.57
    Texas     -2.29
    Oregon    -0.43
    Name: b, dtype: object



## 6. Sorting and Ranking

If we want to sort on key set, we should use function **sort_index( )**:
- For Series


```python
obj = Series(range(4), index = ['a','c','b','d'])
obj.sort_index(ascending = False)
# obj.sort_index()
```




    a    0
    b    2
    c    1
    d    3
    dtype: int64



- For DataFrame


```python
frame = DataFrame(np.arange(8).reshape(2, 4), index = ['three','one'], columns = ['a','c','b','d'])
frame
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
      <th>a</th>
      <th>c</th>
      <th>b</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>three</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>one</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.sort_index()
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
      <th>a</th>
      <th>c</th>
      <th>b</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>three</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.sort_index(axis = 1, ascending = False)
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
      <th>d</th>
      <th>c</th>
      <th>b</th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>three</th>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>one</th>
      <td>7</td>
      <td>5</td>
      <td>6</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



If we want to sort on value set, we should use function **order( )**:


```python
obj = Series([7, -1, 8, 5])
obj.sort_values()
# IN tutorial, there is a function named order(), but caonnot work in jupyter.
```




    1   -1
    3    5
    0    7
    2    8
    dtype: int64



If there are some NAN values, they are actually sorted at last position, like:


```python
obj2 = Series([4, np.nan, 7, np.nan, -1, 3, 12, np.nan])
obj2.sort_values()
```




    4    -1.0
    5     3.0
    0     4.0
    2     7.0
    6    12.0
    1     NaN
    3     NaN
    7     NaN
    dtype: float64



In DataFrame, we can actually sort according to one or more variables, I will it as below:


```python
frame = DataFrame({'a':[5,2,6,3,1], 'b':[-1,0,1,1,2]})
frame.sort_index(by = 'b')
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:2: FutureWarning: by argument to sort_index is deprecated, please use .sort_values(by=...)
      





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
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.sort_index(by = ['b','a']) # ['a','b'] got different result with ['b','a']
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:1: FutureWarning: by argument to sort_index is deprecated, please use .sort_values(by=...)
      """Entry point for launching an IPython kernel.





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
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



In Pandas, we can also a function named **ranking()**, which can be used to generate the rankings:


```python
obj = Series([7, -5, 7, 4,2, 0, 4])
obj.rank()
```




    0    6.5
    1    1.0
    2    6.5
    3    4.5
    4    3.0
    5    2.0
    6    4.5
    dtype: float64



We can also get ranking according to the places of datas in data set.


```python
obj.rank(method = 'first')
```




    0    6.0
    1    1.0
    2    7.0
    3    4.0
    4    3.0
    5    2.0
    6    5.0
    dtype: float64



We can also get ranking according to descending order.


```python
obj.rank(ascending = False, method='max')
```




    0    2.0
    1    7.0
    2    2.0
    3    4.0
    4    5.0
    5    6.0
    6    4.0
    dtype: float64



Still, we can use this function on **DataFrame** data objects, like:


```python
frame = DataFrame({'b':[4.3, 7, -3, 2], 'a':[0,1,0,1],'c':[-2,5,8,-2.5]})
frame
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
      <th>b</th>
      <th>a</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4.3</td>
      <td>0</td>
      <td>-2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.0</td>
      <td>1</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3.0</td>
      <td>0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.0</td>
      <td>1</td>
      <td>-2.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.rank()
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
      <th>b</th>
      <th>a</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.0</td>
      <td>1.5</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.0</td>
      <td>3.5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>1.5</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.0</td>
      <td>3.5</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.rank(axis = 1)
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
      <th>b</th>
      <th>a</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.0</td>
      <td>2.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.0</td>
      <td>1.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.0</td>
      <td>2.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



## 7. Axis Index With Repeating Values

In Series:


```python
obj = Series(range(5), index = ['a','a','b','b','c'])
obj
```




    a    0
    a    1
    b    2
    b    3
    c    4
    dtype: int64




```python
obj.index.is_unique
```




    False




```python
obj['a']
```




    a    0
    a    1
    dtype: int64



When we index in **DataFrame**, we can also do similar operations on that:


```python
df = DataFrame(np.random.randn(4, 3), index = ['a','a','b','b'])
df.ix['a']
```

    /Users/leonardyuan/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:2: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      





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
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>-1.143057</td>
      <td>-0.638386</td>
      <td>1.094285</td>
    </tr>
    <tr>
      <th>a</th>
      <td>0.652737</td>
      <td>-0.163082</td>
      <td>-0.197243</td>
    </tr>
  </tbody>
</table>
</div>


