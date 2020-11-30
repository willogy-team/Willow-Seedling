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

### Object creation

- Creating a `Series` by passing a list of values, letting pandas create a default integer index:
```
>>> s = pd.Series([1, 3, 5, np.nan, 6, 8])
>>> s
0    1.0
1    3.0
2    5.0
3    NaN
4    6.0
5    8.0
dtype: float64
```

- Creating a `DataFrame` by passing a NumPy array, with a datetime index and labeled columns:
```
>>> dates = pd.date_range('20130101', periods=6)
>>> dates
DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
               '2013-01-05', '2013-01-06'],
              dtype='datetime64[ns]', freq='D')
>>> df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list('ABCD'))
>>> df
                   A         B         C         D
2013-01-01  0.620219 -0.183901 -0.485727 -0.304104
2013-01-02  0.106144  0.911428 -0.516627 -0.522257
2013-01-03  0.362659 -0.062068 -1.884467 -0.959284
2013-01-04 -1.954926  1.424344 -1.382519  0.342304
2013-01-05 -0.874978  1.401606  0.331900  1.335983
2013-01-06  1.552202 -0.319846  0.510372 -2.222078
```
- Creating a `DataFrame` by passing a dict of objects that can be converted to series-like.
```
>>> df2 = pd.DataFrame({'A': 1.,
...                     'B': pd.Timestamp('20201130'),
...                     'C': pd.Series(1, index=list(range(4)), dtype='float32'),
...                     'D': np.array([3] * 4, dtype='int32'),
...                     'E': pd.Categorical(["test", "train", "test", "train"]),
...                     'F': 'foo'})
>>> df2
     A          B    C  D      E    F
0  1.0 2020-11-30  1.0  3   test  foo
1  1.0 2020-11-30  1.0  3  train  foo
2  1.0 2020-11-30  1.0  3   test  foo
3  1.0 2020-11-30  1.0  3  train  foo
```

### Viewing data:
- Here is how to view the top and bottom rows of the frame:
```
>>> df.head()
                   A         B         C         D
2013-01-01  0.620219 -0.183901 -0.485727 -0.304104
2013-01-02  0.106144  0.911428 -0.516627 -0.522257
2013-01-03  0.362659 -0.062068 -1.884467 -0.959284
2013-01-04 -1.954926  1.424344 -1.382519  0.342304
2013-01-05 -0.874978  1.401606  0.331900  1.335983
>>> df.tail(2)
                   A         B         C         D
2013-01-05 -0.874978  1.401606  0.331900  1.335983
2013-01-06  1.552202 -0.319846  0.510372 -2.222078
```
- Display the index, columns:
```
>>> df.index
DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
               '2013-01-05', '2013-01-06'],
              dtype='datetime64[ns]', freq='D')
>>> df.columns
Index(['A', 'B', 'C', 'D'], dtype='object')
```

- Converting to a NumPy data. 
```
>>> df.to_numpy()
array([[ 0.62021932, -0.1839012 , -0.48572709, -0.30410424],
       [ 0.106144  ,  0.91142798, -0.51662651, -0.52225711],
       [ 0.36265926, -0.06206815, -1.88446734, -0.95928405],
       [-1.954926  ,  1.4243439 , -1.38251864,  0.34230411],
       [-0.87497755,  1.40160644,  0.33189998,  1.33598272],
       [ 1.55220239, -0.319846  ,  0.51037236, -2.22207821]])
```
NumPy arrays have one dtype for the entire array, while pandas DataFrames have one dtype per column. When you call `DataFrame.to_numpy()`, `pandas` will find the NumPy dtype that can hold all of the dtypes in the DataFrame. This may end up being `object`, which requires casting every value to a Python object.
```
>>> df2.to_numpy()
array([[1.0, Timestamp('2020-11-30 00:00:00'), 1.0, 3, 'test', 'foo'],
       [1.0, Timestamp('2020-11-30 00:00:00'), 1.0, 3, 'train', 'foo'],
       [1.0, Timestamp('2020-11-30 00:00:00'), 1.0, 3, 'test', 'foo'],
       [1.0, Timestamp('2020-11-30 00:00:00'), 1.0, 3, 'train', 'foo']],
      dtype=object)
```
- Showing statistic summary of your data:
```
>>> df.describe()
              A         B         C         D
count  6.000000  6.000000  6.000000  6.000000
mean  -0.031446  0.528594 -0.571178 -0.388239
std    1.226228  0.810859  0.935797  1.201726
min   -1.954926 -0.319846 -1.884467 -2.222078
25%   -0.629697 -0.153443 -1.166046 -0.850027
50%    0.234402  0.424680 -0.501177 -0.413181
75%    0.555829  1.279062  0.127493  0.180702
max    1.552202  1.424344  0.510372  1.335983
```
- Transposing your data:
```
>>> df.T
   2013-01-01  2013-01-02  2013-01-03  2013-01-04  2013-01-05  2013-01-06
A    0.620219    0.106144    0.362659   -1.954926   -0.874978    1.552202
B   -0.183901    0.911428   -0.062068    1.424344    1.401606   -0.319846
C   -0.485727   -0.516627   -1.884467   -1.382519    0.331900    0.510372
D   -0.304104   -0.522257   -0.959284    0.342304    1.335983   -2.222078
```
- Sorting by an axis:
```
>>> df.sort_index(axis=1,ascending=False)
                   D         C         B         A
2013-01-01 -0.304104 -0.485727 -0.183901  0.620219
2013-01-02 -0.522257 -0.516627  0.911428  0.106144
2013-01-03 -0.959284 -1.884467 -0.062068  0.362659
2013-01-04  0.342304 -1.382519  1.424344 -1.954926
2013-01-05  1.335983  0.331900  1.401606 -0.874978
2013-01-06 -2.222078  0.510372 -0.319846  1.552202
```
- Sorting by values:
```
>>> df.sort_values(by='C')
                   A         B         C         D
2013-01-03  0.362659 -0.062068 -1.884467 -0.959284
2013-01-04 -1.954926  1.424344 -1.382519  0.342304
2013-01-02  0.106144  0.911428 -0.516627 -0.522257
2013-01-01  0.620219 -0.183901 -0.485727 -0.304104
2013-01-05 -0.874978  1.401606  0.331900  1.335983
2013-01-06  1.552202 -0.319846  0.510372 -2.222078
```
### Selection

#### Getting

- Selecting a single column, which yields a `Series`, equivalent to df.A:
```
>>> df['A']
2013-01-01    0.620219
2013-01-02    0.106144
2013-01-03    0.362659
2013-01-04   -1.954926
2013-01-05   -0.874978
2013-01-06    1.552202
Freq: D, Name: A, dtype: float64
```

- Selecting via `[]`, which slices the rows.
```
>>> df[0:2]
                   A         B         C         D
2013-01-01  0.620219 -0.183901 -0.485727 -0.304104
2013-01-02  0.106144  0.911428 -0.516627 -0.522257
>>> df['20130103':'20130105']
                   A         B         C         D
2013-01-03  0.362659 -0.062068 -1.884467 -0.959284
2013-01-04 -1.954926  1.424344 -1.382519  0.342304
2013-01-05 -0.874978  1.401606  0.331900  1.335983
```
#### Selection by label

- For getting a cross section using a label:
```
>>> df.loc['20130102']
A    0.106144
B    0.911428
C   -0.516627
D   -0.522257
Name: 2013-01-02 00:00:00, dtype: float64
```

- Selecting on a multi-axis by label:
```
>>> df.loc[:, ['A', 'C']]
                   A         C
2013-01-01  0.620219 -0.485727
2013-01-02  0.106144 -0.516627
2013-01-03  0.362659 -1.884467
2013-01-04 -1.954926 -1.382519
2013-01-05 -0.874978  0.331900
2013-01-06  1.552202  0.510372
```
#### Selection by position

- Select via the position of the passed integers:
```
>>> df.iloc[3]
A   -1.954926
B    1.424344
C   -1.382519
D    0.342304
Name: 2013-01-04 00:00:00, dtype: float64
```
- By integer slices, acting similar to numpy/python:
```
>>> df.iloc[3:5, 0:2]
                   A         B
2013-01-04 -1.954926  1.424344
2013-01-05 -0.874978  1.401606
```

#### Boolean indexing
- Using a single column’s values to select data.
```
>>> df[df['A'] > 0]
                   A         B         C         D
2013-01-01  0.620219 -0.183901 -0.485727 -0.304104
2013-01-02  0.106144  0.911428 -0.516627 -0.522257
2013-01-03  0.362659 -0.062068 -1.884467 -0.959284
2013-01-06  1.552202 -0.319846  0.510372 -2.222078
```
- Selecting values from a DataFrame where a boolean condition is met.
```
>>> df[df > 0]
                   A         B         C         D
2013-01-01  0.620219       NaN       NaN       NaN
2013-01-02  0.106144  0.911428       NaN       NaN
2013-01-03  0.362659       NaN       NaN       NaN
2013-01-04       NaN  1.424344       NaN  0.342304
2013-01-05       NaN  1.401606  0.331900  1.335983
2013-01-06  1.552202       NaN  0.510372       NaN
```

#### Setting 
Setting values by selecting method
```
>>> df.at['20130104','B']=0  # by value
>>> df.iat[0,3]=0  # by position
>>> df.loc[:,'D']=np.array([3]*len(df))  # by assigning with a NumPy array:
>>> df
                   A         B         C  D
2013-01-01  0.620219 -0.183901 -0.485727  3
2013-01-02  0.106144  0.911428 -0.516627  3
2013-01-03  0.362659 -0.062068 -1.884467  3
2013-01-04 -1.954926  0.000000 -1.382519  3
2013-01-05 -0.874978  1.401606  0.331900  3
2013-01-06  1.552202 -0.319846  0.510372  3
```

### Missing data

`pandas` primarily uses the value `np.nan` to represent missing data. It is by default not included in computations. 

Reindexing allows you to change/add/delete the index on a specified axis. This returns a copy of the data.
```
>>> df1 = df.reindex(index=dates[0:4], columns=list(df.columns) + ['E'])
>>> df1.loc[dates[0]:dates[1], 'E'] = 1
>>> df1
                   A         B         C  D    E
2013-01-01  0.620219 -0.183901 -0.485727  3  1.0
2013-01-02  0.106144  0.911428 -0.516627  3  1.0
2013-01-03  0.362659 -0.062068 -1.884467  3  NaN
2013-01-04 -1.954926  0.000000 -1.382519  3  NaN
```
- To drop any rows that have missing data.
```
>>> df1.dropna(how='any')
                   A         B         C  D    E
2013-01-01  0.620219 -0.183901 -0.485727  3  1.0
2013-01-02  0.106144  0.911428 -0.516627  3  1.0
```
- Filling missing data.
```
>>> df1.fillna(value=3.14)
                   A         B         C  D     E
2013-01-01  0.620219 -0.183901 -0.485727  3  1.00
2013-01-02  0.106144  0.911428 -0.516627  3  1.00
2013-01-03  0.362659 -0.062068 -1.884467  3  3.14
2013-01-04 -1.954926  0.000000 -1.382519  3  3.14
```
- To get the boolean mask where values are nan.
```
>>> pd.isna(df1)
                A      B      C      D      E
2013-01-01  False  False  False  False  False
2013-01-02  False  False  False  False  False
2013-01-03  False  False  False  False   True
2013-01-04  False  False  False  False   True
```

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
