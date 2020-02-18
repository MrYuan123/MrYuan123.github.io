---
layout:     post
title:      "Data Science Study Note1"
subtitle:   " \"Hello World, Hello Blog\""
date:       2019-2-13 20:00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Data Science
    
---

# Data Science Study Note1

> Prerequsite:
> As we all know that data science is heat in recent year, thus we all should learn knowledge and skills about data analysis and data mining. 
> 1. First we should study knowledge about Numpy, Pandas, SciPy and SciKit-learn.
> 2. Then, we start learning about Tensorflow, Keras, and Torch.
> 3. Also, we need be familar with basic math concepts like probability, linear algebra.
> So, let's start it.

## 1. Basics of Python

I skip some terms of this chapter beacasue I have used Python before, hence no need to repeat them again. I just share tips about Python.

Python has data set formats like these:
**set**, **list**, **dictionary**, **tuple**

- About **zip** Operation


```python
a = range(10)
b = range(10, 20)
c = zip(a, b)
c
```




    <zip at 0x10b91af08>




```python
for m in c:
    print(m)
```

    (0, 10)
    (1, 11)
    (2, 12)
    (3, 13)
    (4, 14)
    (5, 15)
    (6, 16)
    (7, 17)
    (8, 18)
    (9, 19)


- List comprehensions

This is a kind of useful tools to deal with data set, like this:


```python
x = [1,23,32,8,33,97,123]
```


```python
result = [m if m <30 else 0 for m in x]
result
```




    [1, 23, 0, 8, 0, 0, 0]



- **all** and **any** Operation

This is an useful method to judge whether the elements in a data set match the requirements or not.


```python
conda = [item < 30 for item in x]
```


```python
all(conda)
```




    False




```python
any(conda)
```




    True



we can check the value of variables like this:


```python
%whos
```

    Variable   Type     Data/Info
    -----------------------------
    a          range    range(0, 10)
    b          range    range(10, 20)
    c          zip      <zip object at 0x10b91af08>
    conda      list     n=7
    m          tuple    n=2
    result     list     n=7
    x          list     n=7


- Generate Data Set

**Note**: In Python, funtion can return multi-results


```python
def cal(x, y):
    return (x + y), (x*y), (x/y)
```


```python
a,b,c = cal(10, 5)
a
```




    15




```python
b
```




    50




```python
c
```




    2.0



- **Counter** Collection

This is an useful collection, it inherited from **collections** library, that can be used to count the numbers of elements in a data set, like this:


```python
x = [1,20, 10, 2, 20, 2, 2, 20]
```


```python
from collections import Counter
result = Counter(x)
for key in result:
    print(str(key) + " : " + str(result[key]))
```

    1 : 1
    20 : 3
    10 : 1
    2 : 3


- **Generators**

Actually, I do not often use that, but I must admit that this is useful tool to generate data. It is shown as follows:


```python
def generate_odd(n):
    i = 2
    while i < n: 
        yield i
        i+=2
    
generate_20 = generate_odd(20)
for m in generate_20:
    print(m)
```

    2
    4
    6
    8
    10
    12
    14
    16
    18


- **How to use \*args and **kwargs**


```python
def cal(*args, **kwargs):
    sum = 0
    for m in args:
        sum +=m
    
    for n in kwargs:
        sum+=kwargs[n]
        
    return sum

cal(1,2,3,5,k=12,m=34)
```




    57



## 2. Numpy

Numpy is one of the efficient Library to operate datas, I have studied this before, and I have a study note on my blog. So, I just skip this.

Here is a simple example as follows:


```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
x = np.linspace(0,5,500)
y = np.cos(x)
mplot = plt.plot(x,y)
```

![](/img/in_post/Study_Note/output_34_0.png)



```python
x = np.linspace(0, 10, 1000)
y = np.sin(x)
mplot = plt.plot(x, y)
```

![](/img/in_post/Study_Note/output_35_0.png)

