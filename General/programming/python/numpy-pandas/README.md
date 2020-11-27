# Essential Tutorials for Numpy and pandas

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Nov 27th, 2020 |
| **Topic(s)** | General Techniques |
| **Status**       | In Progress |

# Index 

- Introduction
- Motivation
- Numpy
- Pandas
- Matplotlib

## Introduction

Python is one of the most popular and widely used programming languages and has replaced many programming languages in the industry. The development of libraries has extended python's multi-purpose nature to solve machine learning problems as well. **Numpy** is the fundamental package for scientific computing what is considered as one of the most popular machine learning library in Python. Another ML library is **Pandas** that provides data structures of high-level and a wide variety of tools for analysis. One of the great feature of this library is the ability to translate complex operations with data using one or two commands. Pandas have so many inbuilt methods for grouping, combining data, and filtering, as well as time-series functionality.

## Motivation

Vectorization of `numpy` make code is more concise and easier to read, fewer lines, closely resembles standard mathematical notation, do fast. 

The entire process of manipulating data will be easier if use `pandas`. It support for operations such as re-indexing, iteration, sorting, aggregations, concatenations and visualizations are among the feature highlights of `pandas`. The data manipulation capabilities of `pandas` are built on top of the `numpy` library. 

## Numpy Library

NumPy’s main object is the homogeneous multidimensional array. It is a table of elements (usually numbers), all of the same type, indexed by a tuple of non-negative integers. In NumPy dimensions are called **axes**.

### Numpy's array class

It is called `ndarray` with alias `array`. The more important attributes of an `ndarray` object are:

- **ndarray.ndim**: the number of axes (dimensions) of the array.
    
- **ndarray.shape**: the dimensions of the array. This is a tuple of integers indicating the size of the array in each dimension. For a matrix with n rows and m columns, `shape` will be `(n,m)`. The length of the `shape` tuple is therefore the number of axes, `ndim`.
    
- **ndarray.size**: the total number of elements of the array. This is equal to the product of the elements of `shape`.
    
- **ndarray.dtype**: an object describing the type of the elements in the array. One can create or specify dtype’s using standard Python types. Additionally NumPy provides types of its own. numpy.int32, numpy.int16, and numpy.float64 are some examples.
    
- **ndarray.itemsize**: the size in bytes of each element of the array. For example, an array of elements of type `float64` has `itemsize` 8 (=64/8), while one of type `complex32` has `itemsize` 4 (=32/8). It is equivalent to `ndarray.dtype.itemsize`.
    
- **ndarray.data**: the buffer containing the actual elements of the array. Normally, we won’t need to use this attribute because we will access the elements in an array using indexing facilities.

(E.g.)
```
>>> import numpy as np

>>> a = np.arange(15).reshape(3, 5)

>>> a
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])

>>> a.shape
(3, 5)

>>> a.ndim
2

>>> a.dtype.name
'int64'

>>> a.itemsize
8

>>> a.size
15

>>> type(a)
<class 'numpy.ndarray'>

>>> b = np.array([6, 7, 8])

>>> b
array([6, 7, 8])

>>> type(b)
<class 'numpy.ndarray'>
```
### Loading the library and check its version

```
import numpy as np
np.__version__
````

If you do not install `numpy`, or set up virtual enviroment, please read [link](/General/programming/python/virtualenv)

### Creating arrays

- Create zeros array

```
>>> np.zeros(10, dtype='int')
array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])
```

- Create a n rows by m columns matrix:

```
>>> n, m = 3,5
>>> np.ones((3,5), dtype=float)
array([[ 1.,  1.,  1.,  1.,  1.],
      [ 1.,  1.,  1.,  1.,  1.],
      [ 1.,  1.,  1.,  1.,  1.]])
```

- Create a matrix with a predefined value

```
>>> predefined_value = 1.23
>>> np.full((3,5), predefined_value)
array([[ 1.23,  1.23,  1.23,  1.23,  1.23],
      [ 1.23,  1.23,  1.23,  1.23,  1.23],
      [ 1.23,  1.23,  1.23,  1.23,  1.23]])
```

- Create an array with a set sequence

```
>>> np.arange(0, 20, 2)
array([0, 2, 4, 6, 8,10,12,14,16,18])
```

- Create an array of even space between the given range of values

```
>>> np.linspace(0, 1, 5)
array([ 0., 0.25, 0.5 , 0.75, 1.])
```

- Create an identity matrix

```
>>> np.eye(3)
array([[ 1.,  0.,  0.],
      [ 0.,  1.,  0.],
      [ 0.,  0.,  1.]])
```


## Pandas Library

## Matplotlib

# References
- [Practical Tutorial on Data Manipulation with Numpy and Pandas in Python](https://www.hackerearth.com/practice/machine-learning/data-manipulation-visualisation-r-python/tutorial-data-manipulation-numpy-pandas-python/tutorial/)
- [Essential tutorial-type notebooks on Pandas and Numpy](https://github.com/tirthajyoti/Machine-Learning-with-Python/tree/master/Pandas%20and%20Numpy)
