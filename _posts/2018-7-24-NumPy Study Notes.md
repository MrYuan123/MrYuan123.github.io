---
layout:     post
title:      "NumPy Study Notes"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-7-24 14：00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Mac OS
    - Data Analysis

---

# NumPy Study Notes

## Chapter1 Introduction of Numpy

Numpy is a fundamental package for scientific computing with Python. It contains:

- a powerful N-dimensional array object;
- sophisticated (broadcasting) functions;
- tools for integrating C/C++ and Fortran code;
- useful linear algebra, Fourier transform, and random number capabilities;

We can use NumPy to define a diversity of data types, including multi-dimensioned container of datas.  Thus, NumPy can be used in various areas of data analysis.

NumPy's main object is the homogeneous array, and it is a table indexed by a tuple of positive integers. There is a example as following:

	[[ 1., 0., 0.],
	[ 0., 1., 2.]]

 In NumPy, dimensions are called `axis/axes`. [1,2,3,4] has one axis, and there are three elements in this list, hence we say it has a length of 4. NumPy's array class is called ndarray, which is not same as the array class in Python. `ndnarry` has some attributes as follows:

	[[ 0,  1,  2,  3,  4],
    [ 5,  6,  7,  8,  9],
    [10, 11, 12, 13, 14]]

| Attribute Name | Function | Example Result|
|----------------|:------:|------:|
| ndarray.ndim |the number of axes of this array|3|
| ndarray.shape |the number of dimensions of this array, it is a tuple like (m,n), which indicates the size of the array|(3,5)|
|ndarray.size|the sum of the elements in this array, equal to m*n| 15|
|ndarray.dtype| an object describing the type of the elements in the array, also, NumPy has its own data types like numpy.int32, numpy.float64| 'int64' (ndarray.dtype.name)|
|ndarray.itemsize|the size in bytes of each element of the array, and it is equal to `ndarray.dtype.itemsize`| 8 |
|ndarray.data |the buffer containing the actual elements of the array | \<memory at 0x1062cdb40\>|

**Attention:** The dtype of elements in an array are same.

## Chapter2 The Basics

### 1. How to create array

There are several ways to create arrays.

- We can use Python list or tuple to create an array using `array` function.

	>a = np.array([2,3,4])  --> array([2, 3, 4])

- `array` transforms sequences of sequences into two-dimensional arrays, sequences of sequences of sequences into three-dimensional arrays, and so on.

	> b = np.array([(1.5,2,3), (4,5,6)]). --> array([[ 1.5,  2. ,  3. ],
       [ 4. ,  5. ,  6. ]])

- NumPy offers serveral functions to create arraies with initial content. The function `zeros` creates an array full of zeros, the function `ones` creates an array full of ones, and the function `empty` creates an array whose initial content is random and depends on the state of the memory. By default, the dtype of the created array is float64. Also, dtype can be specified.
	> np.zeros( (3,4) )

	> np.ones( (2,3,4), dtype=np.int16 )

- NumPy provides a function  called `arange` analogous to `range` function in Python, but it returns an array instead of a list.

	> np.arange( 10, 30, 5 ) --> array([10, 15, 20, 25])

- When arange is used with floating point arguments, it is generally not possible to predict the number of elements obtained, due to the finite floating point precision. For this reason, it is usually better to use the function linspace that receives as an argument the number of elements that we want:

	> np.linspace( 0, 2, 9 ) --> array([ 0.  ,  0.25,  0.5 ,  0.75,  1.  ,  1.25,  1.5 ,  1.75,  2.  ])

Other create functions can be found in official Docs.

### 2. How to use basic operations

NumPy offers a plenty of operations on the array, which can promote the efficiency of analyzing data. We can give an example as follow:

	a = np.array( [20,30,40,50] )
	b = np.arange( 4 )

	result:
	a: array( [20,30,40,50] )
	b: array([0, 1, 2, 3])

a. Addition Operation

	$ c = a + b
	$ c
	$ array([20, 29, 38, 47])

b. Square Operation

	$ b**2
	$ array([0, 1, 4, 9])

c. Other Linear Operation

	$ 10*np.sin(a)
	$ array([ 9.12945251, -9.88031624,  7.4511316 , -2.62374854])

d. Judgemnt Operation

	$ a<35
	$ array([ True, True, False, False])

e. `*` Operation	and `dot` Operation

**Attention:** Although in matrix language, `*` operation means matrix product. But in NumPy, the product operation `*` operate elementwise in NumPy arrays. We use `dot` operation to generate the matrix product.

	$ a*b
	$ array([  0,  30,  80, 150])
	$ A = np.array( [[1,1], [0,1]] )
	$ B = np.array( [[2,0], [3,4]] )
	$ A.dot(B)
	$ array([[5, 4],
    ...     [3, 4]])
    $ np.dot(A, B)
    $ array([[5, 4],
    ...     [3, 4]])

f. `+=` and `*=` Operation( just modify existed one, not create new one )

	$ b += 1
	$ array([1,2,3,4])

When operating with arrays of different types, the type of the resulting array corresponds to the more general or precise one.

g. Universal Functions

NumPy provides familiar mathematical functions such as sin, cos, and exp.

	$ B = np.arange(3)
	$ array([0, 1, 2])
	$ array([ 1.        ,  2.71828183,  7.3890561 ])
	$ sqrt() / add() / ....

h. Other Operations

	$ sum() / min() / max()  # get certain element in this array
	$ b = np.arange(12).reshape(3,4)
	$ array([[ 0,  1,  2,  3],
       	  [ 4,  5,  6,  7],
            [ 8,  9, 10, 11]])
	$ b.sum(axis=0)
	$ array([12, 15, 18, 21]) # sum of each column
	$ b.sum(axis=1)
	$ array([ 6, 22, 38])     # sum of each row

Other oerations can be found in official Docs.

### 3. Indexing, Slicing and Iterating

NumPy offers some operations like indexing, slicing and so on, which has the similar functions with Python. One-dimensional arrays are pretty easy, so we skip this part.

Toward multidimensional arrays, they have one index per axis, thus we can find out percise position of certain element according to index tuples. Besides, NumPy offers slicing function on arrays, so we can find sub-arrary in a simple way.

	$ def f(x,y):
	...  return 10*x+y
	$ b = np.fromfunction(f,(5,4),dtype=int)
	b = array([[ 0,  1,  2,  3],
               [10, 11, 12, 13],
               [20, 21, 22, 23],
       		   [30, 31, 32, 33],
       		   [40, 41, 42, 43]])

	$ b[0:5, 1]
	array([ 1, 11, 21, 31, 41])

	$ b[-1]
	array([40, 41, 42, 43])

Sometimes we can use the dots `...` to represent as many colons as needed to produce a complete indexing tuple. Also, we can use realize traversal of the arrays. For example:

	$ for row in b:
	...  print(row)
	[0 1 2 3]
	[10 11 12 13]
	[20 21 22 23]
	[30 31 32 33]
	[40 41 42 43]

**Attention:** If we want to get every element in the array, we can use `np.flat`. The code is 'for element in np.flat:'.


## Chapter3 Shape Manipulation

In a array, the shape of a array means the number of elements along each axis, we can use command `np.shape` to get the shape of a array.

### 1. Change the shape of an array

We can give the following example to illustrate it.

	$ a = np.array([ 2.,  8.,  0.,  6.,  4.,  5.,  1.,  1.,  8.,  9.,  3.,  6.])
	$ a.reshape(3,4)
	array([[2., 8., 0., 6.],
           [4., 5., 1., 1.],
      	   [8., 9., 3., 6.]])
	$ a.reshape(3,4).T
	array([[2., 4., 8.],
           [8., 5., 9.],
           [0., 1., 3.],
           [6., 1., 6.]])

When we use `reshape` command, we just get array's argument with modified shape,.If we want to modify the an array itself, we should use command `resize`,like:

	$ a.resize(2,6)

If a dimension is '-1' in reshape operation, then other dimensions are calculated automatically.

### 2. Stacking together different arrays

a. Vertical

	$ a = np.array([[ 8.,  8.],
       		      [ 0.,  0.]])
	$ b = np.array([[ 1.,  8.],
                    [ 0.,  4.]])
	$ np.vstack((a,b))    		      
	array([[ 8.,  8.],
      	   [ 0.,  0.],
           [ 1.,  8.],
           [ 0.,  4.]])

b. Horizontal

	$ np.hstack((a,b))
	array([[ 8.,  8.,  1.,  8.],
           [ 0.,  0.,  0.,  4.]])

c. stacks 1D arrays as columns into a 2D array

	$ np.column_stack((a,b))

**Attention:** If we want to create an array by stacking along one axis, we can use `r_` or `c_` operation.

### 3. Splitting one array


## Chapter4 Copies and Views

NumPy has some methods to share same data, and there are three cases to introduce these methods.

### 1. Not copy

When we use simple assignments, id doesn't make a copy for existed array objects. Thus, when we use `id()` function, we will get same id.

	$ a = np.arange(12)
	$ b = a
	$ b is a
	True
	# id(a) = id(b)

### 2. View or Shallow Copy

When we use view or shallow copy, we will get different arrays, which share same datas. First, we will introduce `view` method.

	$ c = a.view()
	$ c is a
	False
	$ c.base is a
	True

If we slice a array, we can get a view of sub-array as a return.

### 3. Deep Copy

If we want to get a complete copy of an array and its data, we must use deep copy(`copy` method) to  achieve it.

	$ d = a.copy()
	$ d is a
	Flase
	$ d.base is a
	False


All in all, if we want to know about some other methods on NumPy, we can find relevant explaination in official Docs.

## Chapter5 Fancy Indexing and Index Tricks

Compared with array in Python, NumPy offers more functions on arrays, arrays can be indexes by arrays of numbers or booleans.

### 1. Indexed by Arrays of indices

For one-dimensional arrays, we can get the data in certain position according to arrays of indices, and the result corresponds to the shape of arrays of indices.

	$ a = np.arange(12)**2
	$ i = np.array( [ 1,1,3,8,5 ] )
	$ a[i]                                       
	array([ 1,  1,  9, 64, 25])
	$ i = np.array( [ [ 3, 4], [ 9, 7 ] ] )
	array([[ 9, 16],
           [81, 49]])

For multidimensional arrays, we can also use arrays of indices to get result, but the arrays of indicies for each dimension must have same shape.

	$ a = array([[ 0,  1,  2,  3],
                 [ 4,  5,  6,  7],
      			 [ 8,  9, 10, 11]])

	$ i = np.array([[0,1],
					[1,2]])
	$ j = np.array([[2,1],
					[3,3]])
	$ a[i,j]
	array([[2,5],
           [7,11]])

The classical application of arrays of indices is the search of the maximum value of time-dependent arrays.

We can also use indexing with arrays as a target to assign to:

	$ a = array([0, 1, 2, 3, 4])
	$ a[[1,3,4]] = 0
	$ a
	array([0, 0, 2, 0, 0])
In a similar way, we can use arrays of indices to fulfill further operations on arrays.

	$ a[[0,0,2]]=[1,2,3] # assignment
	$ a[[0,0,2]]+=1      # add

### 2. Indexing with Boolean Arrays

Boolean arrays we can achieve different approaches on array operations. We can pick up specific elements in arrays according to boolean values in arrays. Given  an example as follow:

	$ a = np.arange(12).reshape(3,4)
	$ b = a > 4
	$ b
	array([[False, False, False, False],
       	   [False,  True,  True,  True],
       	   [ True,  True,  True,  True]])
	$ a[b] = 0
	$ a
	array([[0, 1, 2, 3],
           [4, 0, 0, 0],
           [0, 0, 0, 0]])
	# This means that every element higher than 4 becomes 0.

### 3. The ix_() function

## Chpater6 Some tips

### 1. Simple Array Operation

Numpy gives some functions to fulfill linear operations:

	$ a.transpose()        # can achieve the function of transposing matrix
	$ u = np.eye(n)        # get a array with ones on diagonal and zeros elsewhere.

### 2. "Automatic" Reshaping

If you want to change the dimension of an array, you can omit one of the sizes, because numpy can add this size number automatically according to other sizes.

### 3. Vector Stacking

If you want to construct a new array according to two arrays,which have same size, then you can use function `vstack` and `hstack`:

	$ x = np.arange(0,10,2)
	$ y = np.arange(5)
	$ np.vastack(x, y)
	  [[0,2,4,6,8],
       [0,1,2,3,4]]
	$ np.hstack([x,y])
	  [0,2,4,6,8,0,1,2,3,4]

### 4. Histograms

Numpy has a function named `histograms`, which can be used to generate a pair of vectors: the histogram of the array and the vector of bins. So if we want to get histograms, we can use this function. matplotlib also have a similar function to build a histogram, but there is a main difference between them that the histogram function in numpy just generate datas, instead of the diagram.



## Summary

Numpy is an effective pyhton calculation package, if we want to operate scientific calculation, Numpy is the best choice. Further guide of the functions in Numpy can be found in offical website.
