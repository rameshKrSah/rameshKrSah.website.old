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
    
### Creating arrays
Numpy also provides many functions to create arrays:


```python
a = np.zeros((2,2)) # creates an (2, 2) array of all zeros
print(a)

b = np.ones((3, 3)) # creates an (3, 3) array of all ones
print(b)

c = np.full((2, 1), 6) # creates an (2, 1) of all 6's
print(c)

d = np.eye(3) # creates an 3 X 3 identity matrix
print(d)

e = np.random.random((4, 4)) # creates an (4, 4) array filled with random numbers
print(e)

f = np.arange(10) # Creates an array with regularly incrementing values
print(f)

g = np.arange(2, 10, dtype=float) # Creates an array from 2 to 9 with regular step size
print(g)

h = np.arange(2, 3, 0.1) # Creates an array from 2 to less than 3 with step size of .1
print(h)

i = np.linspace(1., 4., 6) # creates an array with 6 elements, and spaced equally between 1.0 and 4.0
print(i)

j = np.indices((2,2)) # creates a set of arrays, one per dimension with each representing variation in that dimension
print(j)
```

    [[0. 0.]
     [0. 0.]]
    [[1. 1. 1.]
     [1. 1. 1.]
     [1. 1. 1.]]
    [[6]
     [6]]
    [[1. 0. 0.]
     [0. 1. 0.]
     [0. 0. 1.]]
    [[0.63585344 0.57184944 0.87038554 0.35211488]
     [0.63314327 0.78081324 0.76938605 0.92236638]
     [0.88295181 0.99477054 0.79406022 0.06707455]
     [0.81003558 0.8224512  0.30867579 0.58384974]]
    [0 1 2 3 4 5 6 7 8 9]
    [2. 3. 4. 5. 6. 7. 8. 9.]
    [2.  2.1 2.2 2.3 2.4 2.5 2.6 2.7 2.8 2.9]
    [1.  1.6 2.2 2.8 3.4 4. ]
    [[[0 0]
      [1 1]]
    
     [[0 1]
      [0 1]]]
    

### Indexing and accessing arrays
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

b = a[:2, 1:3] # use the slice to pull out the subarray consisting the first 2 rows of a and columns 1 and 2
print(b.shape)
print(b)

# A slice of an array is a view into the same data, so modifying it will modify the original array.
print(a[0,1])
b[0,0] = 77
print(a[0,1])
```

    (3, 4)
    [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]]
    (2, 2)
    [[2 3]
     [6 7]]
    2
    77
    


Two ways of accessing the data in the middle row of the array.  
Mixing integer indexing with slices yields an array of lower rank, while using only the slices yields an array of the same rank as the original array.


```python
a = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])

row_1 = a[1, :] # rank 1 view of the second row of a
row_2 = a[1:2, :] # rank 2 view of the seocnd row of a
print(row_1, row_1.shape)
print(row_2, row_2.shape)

# we can make the same distinction when accessing the columns of the array
col_1 = a[:, 1]
col_2 = a[:, 1:2]
print(col_1, col_1.shape)
print(col_2, col_2.shape)
```

    [5 6 7 8] (4,)
    [[5 6 7 8]] (1, 4)
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

# An example of integer array indexing
# The returned array has shape (3,)
print(a[[0, 1, 2],[0,1,0]])

# The above example of array indexing is equivalent to this 
print(np.array([a[0,0], a[1,1], a[2,0]]))

```

    [[1 2]
     [3 4]
     [5 6]]
    (3, 2)
    [1 4 5]
    [1 4 5]
    

One useful trick with intger array indexing is selecting or mutating one element from each row of matrix.


```python
a = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
print(a)

# Create and array of the indices
b = np.array([0, 2, 0, 1])

# select one element from each row of a using the indices in b
print(a[np.arange(4), b])

# Mutate one element from each row of a using the indices in b
a[np.arange(4), b] += 10
print(a)
```

    [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]
    [ 1  6  7 11]
    [[11  2  3]
     [ 4  5 16]
     [17  8  9]
     [10 21 12]]
    

### Datatypes   
Every numpy array is a grid of elements of the same type. We can let numpy decide the datatype for us or we can specify them ourselves.


```python
x = np.array([1, 2])
print(x.dtype)

y = np.array([1,2], dtype=np.int64)
print(y.dtype)
```

    int32
    int64
    

### Array math  
Basic mathematical functions operate elementwise on arrays, and are available both as operator overloads and as functions.


```python
x = np.array([[1,2],[3,4]], dtype=np.float64)
y = np.array([[5,6],[7,8]], dtype=np.float64)


# Elementwise sum, both produces a new array
print(x + y)
print(np.add(x, y))

# Elementwise difference, both produces a new array
print(x - y)
print(np.subtract(x, y))

# Elementwise product, both produces a new array
print(x * y)
print(np.multiply(x, y))

# Elementwise division, both produces a new array
print(x / y)
print(np.divide(x, y))

#Elementwise square root
print(np.sqrt(x))
```

    [[ 6.  8.]
     [10. 12.]]
    [[ 6.  8.]
     [10. 12.]]
    [[-4. -4.]
     [-4. -4.]]
    [[-4. -4.]
     [-4. -4.]]
    [[ 5. 12.]
     [21. 32.]]
    [[ 5. 12.]
     [21. 32.]]
    [[0.2        0.33333333]
     [0.42857143 0.5       ]]
    [[0.2        0.33333333]
     [0.42857143 0.5       ]]
    [[1.         1.41421356]
     [1.73205081 2.        ]]
    


To form the inner / dot product between a vector / matrix and a vector / matrix we use the dot operator. dot operator is  available both as a function in the module and as an instance method of array objects.


```python

x = np.array([[1,2],[3,4]])
y = np.array([[5,6],[7,8]])

v = np.array([9,10])
w = np.array([11, 12])

# Inner product of vectors
print(v.dot(w))
print(np.dot(v, w))

# Inner product of a matrix and a vector
print(x.dot(v))
print(np.dot(x, v))

# Inner product of matrices
print(x.dot(y))
print(np.dot(x, y))
```

    219
    219
    [29 67]
    [29 67]
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
    

### Broadcasting  
Broadcasting is a powerful mechanism that allows numpy to work with arrays of different shapes when performing arthimetic operations. Frequently we have a smaller array and a larger array, and we want to use the smaller array multiple times to perform some operations on the larger array. Here, broadcasting comes into play.


```python
# For example say we want to add a constant vector v to each row of a matrix x. We could do it like this

# we will add the vector v to each row of the matrix x, stroring the result in the matrix y
x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
v = np.array([1, 0, 1])
print(x.shape, x)
print(v.shape, v)

# Create an empty matrix with the same shape as x
y = np.empty_like(x)

# Add the vector v to each row of the matrix with an explicit loop
for i in range(4):
    y[i,:] = x[i, :] + v
    
    
print(y)
```

    (4, 3) [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]
    (3,) [1 0 1]
    [[ 2  2  4]
     [ 5  5  7]
     [ 8  8 10]
     [11 11 13]]
    

This works; however when the martix is large this approach is slow. Now lets see how we can do this using the numpy boradcasting.


```python
y = x + v
print(y)
```

    [[ 2  2  4]
     [ 5  5  7]
     [ 8  8 10]
     [11 11 13]]
    

That's it!  
The line y = x + v works even though x has shape(4, 3) and v has shape (3,) due to broadcasting; this line works as if v actually had shape (4, 3), where each row was a copy of v, and the sum was performed elementwise.  

Broadcasting two arrays together follows these rules:  
1. If the array do not have the same rank, prepend the shape of the lower rank array with 1's until both shapes have the same length.
2. The two arrays are said to be compatible in a dimension if they have the same size in the dimension, or if one of the arrays has size 1 in that dimension.
3. The arrays can be broadcast together if they are compatible in all dimensions.
4. After broadcasting, each arrays behaves as if it had shape equal to the elementwise maximum of shapes of the two input array.
5. In any dimension where one array had size 1 and the other array had size greater than 1, the first array behaves as if it were copied along that dimension.

Function that support braodcasting are known as **universal funcions**. The full list of universal functions is available [here](https://docs.scipy.org/doc/numpy/reference/ufuncs.html#available-ufuncs)

### Array manipulation [routines](https://docs.scipy.org/doc/numpy/reference/routines.array-manipulation.html) 
* Reshaping an array : gives a new shape to an array without changing its data

```python
a = np.arange(6)
print(a.shape, a)

# reshape into a (3, 2) array
b = a.reshape(3, 2)
print(b.shape, b)

# reshape into a (2, 3) array
c = a.reshape(2, 3)
print(c.shape, c)

# The order keyword gives the index ordering both for fetching the values from a, and then placing the values into the output
# array. By default the order is 'C' i.e., C like indexing
d = a.reshape((3, 2), order='F') # Fortran-like indexing
print(d.shape, d)

e = np.reshape(b, 6)
print(e.shape, e)

f = np.reshape(b, 6, order='F')
print(f.shape, f)

```

    (6,) [0 1 2 3 4 5]
    (3, 2) [[0 1]
     [2 3]
     [4 5]]
    (2, 3) [[0 1 2]
     [3 4 5]]
    (3, 2) [[0 3]
     [1 4]
     [2 5]]
    (6,) [0 1 2 3 4 5]
    (6,) [0 2 4 1 3 5]
    


* Ravel : Returns a contiguous falttened array. Returns a 1-D array

```python
x = np.array([[1, 2, 3], [4, 5, 6]])
print(x.shape, x)

# flatten the array x in to one-dimension
a = x.ravel()
print(a.shape, a)

print(x.reshape(-1))

print(np.ravel(x.T)) # The T operator computes the transpose of the array x

# different ordering modes 
print(np.ravel(x, order='F'))

print(np.ravel(x, order='C'))

print(np.ravel(x, order='K'))
```

    (2, 3) [[1 2 3]
     [4 5 6]]
    (6,) [1 2 3 4 5 6]
    [1 2 3 4 5 6]
    [1 4 2 5 3 6]
    [1 4 2 5 3 6]
    [1 2 3 4 5 6]
    [1 2 3 4 5 6]
    

* Flat : Returns a 1-D iterator over the array

```python
x = np.arange(1, 7).reshape(2, 3)
print(x)

# get the 1-D array of x
a = x.flat
print(type(a))
print(a[3])

# assignment example
x.flat = 3
print(x)

x.flat[[1, 4]] = 1
print(x)
```

    [[1 2 3]
     [4 5 6]]
    <class 'numpy.flatiter'>
    4
    [[3 3 3]
     [3 3 3]]
    [[3 1 3]
     [3 1 3]]
    


* Flatten : Returns a copy of the array collapsed into one dimension

```python
a = np.array([[1, 2], [3, 4]])
print(a)

b = a.flatten()
print(type(b))
print(b)

c = a.flatten(order='F')
print(c)


```

    [[1 2]
     [3 4]]
    <class 'numpy.ndarray'>
    [1 2 3 4]
    [1 3 2 4]
    


* Transpose : Compute the transpose 

```python
x = np.arange(4).reshape(2, 2)
print(x)

y = x.transpose()
print(y)

x = np.ones((1, 2, 3))
print(x)

y = np.transpose(x, (1, 0, 2))
print(y)
```

    [[0 1]
     [2 3]]
    [[0 2]
     [1 3]]
    [[[1. 1. 1.]
      [1. 1. 1.]]]
    [[[1. 1. 1.]]
    
     [[1. 1. 1.]]]
    


* Swapaxes : interchange two axes of an array

```python
x = np.array([[1, 2, 3]])
print(x)

y = x.swapaxes(0, 1)
print(y)

x = np.array([[[0,1],[2,3]],[[4,5],[6,7]]])
print(x)

y = x.swapaxes(0, 2)
print(y)

```

    [[1 2 3]]
    [[1]
     [2]
     [3]]
    [[[0 1]
      [2 3]]
    
     [[4 5]
      [6 7]]]
    [[[0 4]
      [2 6]]
    
     [[1 5]
      [3 7]]]
    


* Creating arrays by speciying minimum dimension

```python
a = np.atleast_1d([1, 2])
print(a)
print(a.shape)

b = np.atleast_2d([1, 2])
print(b)
print(b.shape)

c = np.atleast_3d([1, 2])
print(c)
print(c.shape)
```

    [1 2]
    (2,)
    [[1 2]]
    (1, 2)
    [[[1]
      [2]]]
    (1, 2, 1)
    


* Expanding and squeezing the shape of arrays

```python
x = np.array([1, 2])  # x has two axis here, axis = 0 is columns and axis = 1 is row
print(x)
print(x.shape)

y = np.expand_dims(x, axis = 0)
print(y)
print(y.shape)

z = np.expand_dims(x, axis = 1)
print(z)
print(z.shape)

# Lets see some example for removing single-dimension entries from the shape of an array
x = np.array([[[0], [1], [2]]])
print(x)
print(x.shape) # only the axis with value 1 can be squeezed

y = np.squeeze(x)
print(y)
print(y.shape)

z = np.squeeze(x, axis = 0)
print(z)
print(z.shape)

z = np.squeeze(x, axis = 2)
print(z)
print(z.shape)
```

    [1 2]
    (2,)
    [[1 2]]
    (1, 2)
    [[1]
     [2]]
    (2, 1)
    [[[0]
      [1]
      [2]]]
    (1, 3, 1)
    [0 1 2]
    (3,)
    [[0]
     [1]
     [2]]
    (3, 1)
    [[0 1 2]]
    (1, 3)
    


* Splitting an array

```python
# 1. Split : Split an array into multiple sub-arrays
x = np.arange(9.0)
print(x)

# Split the array x into 3 parts
y = np.split(x, 3)
print(y)

# Split the array x with the split position in an 1-D array, this array must be sorted 
z = np.split(x, [2, 4, 6, 8])
print(z)

# 2. hsplit : Split an array into multiple sub-arrays horizontally i.e., column-wise
x = np.arange(16.0).reshape(4, 4)
print(x)

# horizontal split with at max 2 columns
y = np.hsplit(x, 2)
print(y)

# 3. vsplit : SPlit an array into multiple sub-arrays vertically i.e., row-wise
x = np.arange(16.0).reshape(4, 4)
print(x)

# vertical split with two rows
y = np.vsplit(x, 2)
print(y)

```

    [0. 1. 2. 3. 4. 5. 6. 7. 8.]
    [array([0., 1., 2.]), array([3., 4., 5.]), array([6., 7., 8.])]
    [array([0., 1.]), array([2., 3.]), array([4., 5.]), array([6., 7.]), array([8.])]
    [[ 0.  1.  2.  3.]
     [ 4.  5.  6.  7.]
     [ 8.  9. 10. 11.]
     [12. 13. 14. 15.]]
    [array([[ 0.,  1.],
           [ 4.,  5.],
           [ 8.,  9.],
           [12., 13.]]), array([[ 2.,  3.],
           [ 6.,  7.],
           [10., 11.],
           [14., 15.]])]
    [[ 0.  1.  2.  3.]
     [ 4.  5.  6.  7.]
     [ 8.  9. 10. 11.]
     [12. 13. 14. 15.]]
    [array([[0., 1., 2., 3.],
           [4., 5., 6., 7.]]), array([[ 8.,  9., 10., 11.],
           [12., 13., 14., 15.]])]
    


* Adding and removing elements

```python
# 1. delete : Return a new array with sub-arrys along an axis deleted. 
x = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
print(x)

# delete first sub-array along the axis = 0 i.e., columns
y = np.delete(x, 1, 0)
print(y)

# delete the second sub-array along the axis  = 1 i.e, row
z = np.delete(x, 2, 1)
print(z)

# 2. insert : Insert values along the given axis before the given indices
a = np.array([[1, 1], [2, 2], [3, 3]])
print(a)

#insert 5 at positon 1, with array flatten. If axis is not given the array will be flatten first before inserting
y = np.insert(a, 1, 5)
print(y)

# insert 5 at position 1 along the row axis
z = np.insert(a, 1, 5, axis=1)
print(z)

# insert 5 at position 1 along the column axis
p = np.insert(a, 1, 5, axis=0)
print(p)

# 3. append : Append values to the end of an array.
a = np.array([[1, 1], [2, 2], [3, 3]])
print(a)

# append data with the original array flattned
y = np.append(a, [[4, 4], [5, 5]])
print(y)

# append along the column
y = np.append(a, [[4, 4], [5, 5]], axis=0)
print(y)


# 4. resize : return a new array with the specified shape
a = np.array([[0,1],[2,3]])
print(a)

print(np.resize(a, (2, 3)))
```

    [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]]
    [[ 1  2  3  4]
     [ 9 10 11 12]]
    [[ 1  2  4]
     [ 5  6  8]
     [ 9 10 12]]
    [[1 1]
     [2 2]
     [3 3]]
    [1 5 1 2 2 3 3]
    [[1 5 1]
     [2 5 2]
     [3 5 3]]
    [[1 1]
     [5 5]
     [2 2]
     [3 3]]
    [[1 1]
     [2 2]
     [3 3]]
    [1 1 2 2 3 3 4 4 5 5]
    [[1 1]
     [2 2]
     [3 3]
     [4 4]
     [5 5]]
    [[0 1]
     [2 3]]
    [[0 1 2]
     [3 0 1]]
    
