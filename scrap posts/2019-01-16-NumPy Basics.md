---
title: 	"NumPy Basics"
date: 	2019-01-16
mathjax: True
tags: 	[machine_learning]
---

# Introduction to NumPy "Numerical Python"

In this example we will exlore the basic and fundamental usage of [NumPy](https://www.numpy.org/) package. NumPy is the 
fundamental package used for scientific computing with Python. The data container used in NumPy is the numpy array. 
A numpy array is a grid of values, all the same type, and is indexed by a tuple of non-negative integers. The number of dimensions is the rank of the array; the shape of the array is a tuple of integers giving the size of the array along each dimension.

We can initialize numpy arrays from nested Python lists, and access the elements using square brackets.


```python
import numpy as np

a = np.array([1, 2, 3])
print(type(a))
print(a.shape)
print(a[0], a[1], a[2])
a[0] = 5
print(a)
```

    <class 'numpy.ndarray'>
    (3,)
    1 2 3
    [5 2 3]
    


```python
b = np.array([[1,2,3],[4, 5, 6]])
print(b.shape)
print(b[0,0], b[0,1], b[1,0])
```

    (2, 3)
    1 2 4
    

Numpy also provides many functions to create arrays:


```python
a = np.zeros((2,2)) # creates an (2, 2) array of all zeros
print(a)

```

    [[0. 0.]
     [0. 0.]]
    


```python
b = np.ones((3, 3)) # creates an (3, 3) array of all ones
print(b)

```

    [[1. 1. 1.]
     [1. 1. 1.]
     [1. 1. 1.]]
    


```python
c = np.full((2, 1), 6) # creates an (2, 1) of all 6's
print(c)

```

    [[6]
     [6]]
    


```python
d = np.eye(3) # creates an 3 X 3 identity matrix
print(d)

```

    [[1. 0. 0.]
     [0. 1. 0.]
     [0. 0. 1.]]
    


```python
e = np.random.random((4, 4)) # creates an (4, 4) array filled with random numbers
print(e)

```

    [[0.94146333 0.83125537 0.75444578 0.02354831]
     [0.62300056 0.09951494 0.75073056 0.69531148]
     [0.88696859 0.52434326 0.10436071 0.88583056]
     [0.53745898 0.18896284 0.71874308 0.12699926]]
    


```python
f = np.arange(10) # Creates an array with regularly incrementing values
print(f)

```

    [0 1 2 3 4 5 6 7 8 9]
    


```python
g = np.arange(2, 10, dtype=float) # Creates an array from 2 to 9 with regular step size
print(g)

```

    [2. 3. 4. 5. 6. 7. 8. 9.]
    


```python
h = np.arange(2, 3, 0.1) # Creates an array from 2 to less than 3 with step size of .1
print(h)

```

    [2.  2.1 2.2 2.3 2.4 2.5 2.6 2.7 2.8 2.9]
    


```python
i = np.linspace(1., 4., 6) # creates an array with 6 elements, and spaced equally between 1.0 and 4.0
print(i)

```

    [1.  1.6 2.2 2.8 3.4 4. ]
    


```python
j = np.indices((2,2)) # creates a set of arrays, one per dimension with each representing variation in that dimension
print(j)
```

    [[[0 0]
      [1 1]]
    
     [[0 1]
      [0 1]]]
    


```python
k = np.random.randint(0, 100, size=(3, 5)) # creates a numpy random integer array of size (3, 5) from 0 to 100 
print(k)
```

    [[41 69 83 78  0]
     [32 19 55 27 40]
     [ 8 60 32 67 11]]
    

## Indexing and Accessing
Numpy allows several ways to index an arrays.
1. Slicing  
Similar to Python lists, numpy arrays can be sliced, and we must speciy the slice for each dimension. We can mix intger indexing with slice indexing, but this will yield an array of lower rank than the original array.


```python
# Create the following rank 2 array with shape (3, 4)
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
a = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
print(a.shape)
print(a)
```

    (3, 4)
    [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]]
    


```python
b = a[:2, 1:3] # use the slice to pull out the subarray consisting the first 2 rows of a and columns 1 and 2
print(b.shape)
print(b)

```

    (2, 2)
    [[2 3]
     [6 7]]
    


```python
# A slice of an array is a view into the same data, so modifying it will modify the original array.
print(a[0,1])
b[0,0] = 77
print(a[0,1])
```

    2
    77
    

Two ways of accessing the data in the middle row of the array. **Mixing integer indexing with slices** yields an array of lower rank, while using only the slices yields an array of the same rank as the original array.


```python
a = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])

row_1 = a[1, :] # rank 1 view of the second row of a
row_2 = a[1:2, :] # rank 2 view of the seocnd row of a
print(row_1, row_1.shape)
print(row_2, row_2.shape)

```

    [5 6 7 8] (4,)
    [[5 6 7 8]] (1, 4)
    


```python
# we can make the same distinction when accessing the columns of the array
col_1 = a[:, 1]
col_2 = a[:, 1:2]
print(col_1, col_1.shape)
print(col_2, col_2.shape)
```

    [ 2  6 10] (3,)
    [[ 2]
     [ 6]
     [10]] (3, 1)
    

2. Integer array indexing  
When we use the slice indexing to index, the resulting array view will always be a subarray of the original array. In contrast, integer array indexing allows us to construct arbitrary arrays using the data from the another array.


```python
a = np.array([[1,2],[3,4],[5,6]])
print(a)
print(a.shape)
```

    [[1 2]
     [3 4]
     [5 6]]
    (3, 2)
    


```python
# An example of integer array indexing
# The returned array has shape (3,)
print(a[[0, 1, 2],[0,1,0]])

```

    [1 4 5]
    


```python
# The above example of array indexing is equivalent to this 
print(np.array([a[0,0], a[1,1], a[2,0]]))
```

    [1 4 5]
    

One useful trick with intger array indexing is selecting or mutating one element from each row of matrix.


```python
a = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
print(a)

# Create and array of the indices
b = np.array([0, 2, 0, 1])
```

    [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]
    


```python
# select one element from each row of a using the indices in b
print(a[np.arange(4), b])

```

    [ 1  6  7 11]
    


```python
# Mutate one element from each row of a using the indices in b
a[np.arange(4), b] += 10
print(a)
```

    [[11  2  3]
     [ 4  5 16]
     [17  8  9]
     [10 21 12]]
    

## Datatypes  
Every numpy array is a grid of elements of the same type. We can let numpy decide the datatype for us or we can specify them ourselves.


```python
x = np.array([1, 2])
print(x.dtype)

y = np.array([1,2], dtype=np.int64)
print(y.dtype)
```

    int32
    int64
    

## Array math  
Basic mathematical functions operate elementwise on arrays, and are available both as operator overloads and as functions.


```python
x = np.array([[1,2],[3,4]], dtype=np.float64)
y = np.array([[5,6],[7,8]], dtype=np.float64)

print(x)
print(y)
```

    [[1. 2.]
     [3. 4.]]
    [[5. 6.]
     [7. 8.]]
    


```python
# Elementwise sum, both produces a new array
print(x + y)
print(np.add(x, y))

```

    [[ 6.  8.]
     [10. 12.]]
    [[ 6.  8.]
     [10. 12.]]
    


```python
# Elementwise difference, both produces a new array
print(x - y)
print(np.subtract(x, y))

```

    [[-4. -4.]
     [-4. -4.]]
    [[-4. -4.]
     [-4. -4.]]
    


```python
# Elementwise product, both produces a new array
print(x * y)
print(np.multiply(x, y))

```

    [[ 5. 12.]
     [21. 32.]]
    [[ 5. 12.]
     [21. 32.]]
    


```python
# Elementwise division, both produces a new array
print(x / y)
print(np.divide(x, y))

```

    [[0.2        0.33333333]
     [0.42857143 0.5       ]]
    [[0.2        0.33333333]
     [0.42857143 0.5       ]]
    


```python
#Elementwise square root
print(np.sqrt(x))
```

    [[1.         1.41421356]
     [1.73205081 2.        ]]
    

To form the inner ot dot product between a vector and matrix or a matrix and vector we use the dot operator. Dot operator is available both as a function in the module and as an instance method of array objects.


```python
x = np.array([[1,2],[3,4]])
y = np.array([[5,6],[7,8]])

v = np.array([9,10])
w = np.array([11, 12])


```


```python
# Inner product of vectors
print(v.dot(w))
print(np.dot(v, w))
```

    219
    219
    


```python
# Inner product of a matrix and a vector
print(x.dot(v))
print(np.dot(x, v))

```

    [29 67]
    [29 67]
    


```python
# Inner product of matrices
print(x.dot(y))
print(np.dot(x, y))
```

    [[19 22]
     [43 50]]
    [[19 22]
     [43 50]]
    

Numpy provides many useful math functions for performing computations on arrays.
[A comprehensive list of all math functions](https://docs.scipy.org/doc/numpy/reference/routines.math.html)


```python
x = np.array([[1, 2], [3, 4]])

print(np.sum(x)) # computes sum of all elements
print(np.sum(x, axis = 0)) # computes sum of each columns
print(np.sum(x, axis=1)) # computes sum of each row

print(np.prod(x)) # computes the product of all elements
print(np.prod(x, axis=1)) # computes the product of rows
print(np.prod(x, axis=0)) # computes the product of columns
```

    10
    [4 6]
    [3 7]
    24
    [ 2 12]
    [3 8]
    


