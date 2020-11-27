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

### Array Creating

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

### Array Indexing

- In a one-dimensional array, can access value from index as `list`:

```
>>> x1 = np.array([4, 3, 4, 4, 8, 4])
>>> x1
array([4, 3, 4, 4, 8, 4])

#assess value from index zero
>>> x1[0]
4

#assess fifth value
>>> x1[4]
8

#get the last value
>>> x1[-1]
4

#get the second last value
>>> x1[-2]
8
```

- In a multidimensional array, we need to specify row and column index:

```
>>> x2
array([[3, 7, 5, 5],
      [0, 1, 5, 9],
      [3, 0, 5, 0]])


#1st row and 2nd column value
>>> x2[2,3]
0

#3rd row and last value from the 3rd column
>>> x2[2,-1]
0


#replace value at 0,0 index
>>> x2[0,0] = 12
>>> x2
array([[12,  7,  5,  5],
      [ 0,  1,  5,  9],
      [ 3,  0,  5,  0]])
```

### Array Slicing
You base array indexing with `list` slicing behaviors can do.

```
>>> x=np.arange(15).reshape((3,5))
>>> x
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])

#from start to 1th position rows
>>> x[:2,]
array([[0, 1, 2, 3, 4],
       [5, 6, 7, 8, 9]])

#from 2th to 3th position collumns
>>> x[:,2:4] 
array([[ 2,  3],
       [ 7,  8],
       [12, 13]])
```

### Array Concatenation

```
#You can concatenate two or more arrays at once.
>>> x = np.array([1, 2, 3])
>>> y = np.array([3, 2, 1])
>>> z = [21,21,21]
>>> np.concatenate([x, y,z])
array([ 1,  2,  3,  3,  2,  1, 21, 21, 21])


#You can also use this function to create 2-dimensional arrays.
>>> grid = np.array([[1,2,3],[4,5,6]])
>>> np.concatenate([grid,grid])
array([[1, 2, 3],
      [4, 5, 6],
      [1, 2, 3],
      [4, 5, 6]])


#Using its axis parameter, you can define row-wise or column-wise matrix
>>> np.concatenate([grid,grid],axis=1)
array([[1, 2, 3, 1, 2, 3],
      [4, 5, 6, 4, 5, 6]])
```
```
>>> x = np.array([3,4,5])
>>> grid = np.array([[1,2,3],[17,18,19]])
>>> np.vstack([x,grid])
array([[ 3,  4,  5],
      [ 1,  2,  3],
      [17, 18, 19]])


#Similarly, you can add an array using np.hstack
>>> z = np.array([[9],[9]])
>>> np.hstack([grid,z])
array([[ 1,  2,  3,  9],
      [17, 18, 19,  9]])
```

### Numpy Matrix Calculating

## Pandas Library

`pandas` is well suited for many different kinds of data:

- Tabular data with heterogeneously-typed columns, as in an SQL table or Excel spreadsheet.
- Ordered and unordered (not necessarily fixed-frequency) time series data.
- Arbitrary matrix data (homogeneously typed or heterogeneous) with row and column labels.
- Any other form of observational / statistical data sets. The data actually need not be labeled at all to be placed into a pandas data structure.

### Data structures
| Dimensions | Name | Description |
| --|---|----------------|
|1|Series| 1D labeled homogeneously-typed array|
|2|DataFrame|General 2D labeled, size-mutable tabular structure with potentially heterogeneously-typed |

### Pandas capabilities:

- Easy handling of missing data (represented as NaN) in floating point as well as non-floating point data
- Size mutability: columns can be inserted and deleted from DataFrame and higher dimensional objects
- Automatic and explicit data alignment: objects can be explicitly aligned to a set of labels, or the user can simply ignore the labels and let Series, DataFrame, etc. automatically align the data for you in computations
- Powerful, flexible group by functionality to perform split-apply-combine operations on data sets, for both aggregating and transforming data
- Make it easy to convert ragged, differently-indexed data in other Python and NumPy data structures into DataFrame objects
- Intelligent label-based slicing, fancy indexing, and subsetting of large data sets
- Intuitive merging and joining data sets
- Flexible reshaping and pivoting of data sets
- Hierarchical labeling of axes (possible to have multiple labels per tick)
- Robust IO tools for loading data from flat files (CSV and delimited), Excel files, databases, and saving / loading data from the ultrafast HDF5 format
- Time series-specific functionality: date range generation and frequency conversion, moving window statistics, date shifting and lagging.

#### What kind of data does pandas handle?

#### How do I read and write tabular data?

#### How do I select a subset of a DataFrame?

#### How to create plots in pandas?

#### How to create new columns derived from existing columns?

#### How to calculate summary statistics?

#### How to reshape the layout of tables?

#### How to combine data from multiple tables?

#### How to handle time series data with ease?

#### How to manipulate textual data?

# References
- [Practical Tutorial on Data Manipulation with Numpy and Pandas in Python](https://www.hackerearth.com/practice/machine-learning/data-manipulation-visualisation-r-python/tutorial-data-manipulation-numpy-pandas-python/tutorial/)
- [Essential Tutorial-type Notebooks on Pandas and Numpy](https://github.com/tirthajyoti/Machine-Learning-with-Python/tree/master/Pandas%20and%20Numpy)
- [Pandas Documentation](https://pandas.pydata.org/docs/getting_started/intro_tutorials/01_table_oriented.html)
