---
title: 	"NumPy Array Manipulation"
date: 	2019-01-24
mathjax: True
tags: 	[machine_learning]
---


# NumPy Array manipulation 
We can perform various operations to change propertise of a NumPy array. [All the manipulation routines can be found here.](https://docs.scipy.org/doc/numpy/reference/routines.array-manipulation.html) We will explore some of them.


```python
# Reshaping an array : gives a new shape to an array without changing its data
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
    


```python
# Ravel : Returns a contiguous falttened array. Returns a 1-D array
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
    


```python
# Flat : Returns a 1-D iterator over the array
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
    


```python
# Flatten : Returns a copy of the array collapsed into one dimension
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
    


```python
# Transpose : Compute the transpose 
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
    


```python
# swapaxes : interchange two axes of an array
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
    


```python
# Creating arrays by speciying minimum dimension
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
    


```python
# Expanding and squeezing the shape of arrays
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
    


```python
# Splitting an array
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
    


```python
# Adding and removing elements
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
    


```python
np.random.normal(0, 1, (100, 561))
```




    array([[ 0.46600113,  0.08725254, -0.01743358, ..., -1.92789952,
             0.66982862, -0.38115274],
           [-0.60490657, -0.23436994, -0.16278985, ...,  0.35812715,
             0.80336374, -1.36715237],
           [ 0.24409704, -1.87229175,  0.16623769, ..., -0.55053441,
            -0.37469977,  1.08444909],
           ...,
           [-0.53157555, -0.03298659, -0.23910657, ...,  0.0804611 ,
            -1.36207628,  1.6683774 ],
           [ 0.90771193,  0.73341408,  1.45951961, ..., -0.36493613,
            -1.81678354, -0.73792662],
           [ 0.60220492,  1.29839034, -0.81676864, ..., -0.11190615,
            -0.5941561 , -0.13481428]])


