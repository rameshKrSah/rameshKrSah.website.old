---
title: 	"NumPy Array Manipulation"
date: 	2019-01-24
mathjax: True
tags: 	[machine_learning]
---


# NumPy Array manipulation 
We can perform various operations to change propertise of a NumPy array. [All the manipulation routines can be found here.](https://docs.scipy.org/doc/numpy/reference/routines.array-manipulation.html) We will explore some of them.

* Reshaping an array : gives a new shape to an array without changing its data


```python
a = np.arange(6)
print(a.shape, a)
```

    (6,) [0 1 2 3 4 5]
    


```python
# reshape into a (3, 2) array
b = a.reshape(3, 2)
print(b.shape, b)
```

    (3, 2) [[0 1]
     [2 3]
     [4 5]]
    


```python
# reshape into a (2, 3) array
c = a.reshape(2, 3)
print(c.shape, c)

```

    (2, 3) [[0 1 2]
     [3 4 5]]
    

The order keyword gives the index ordering both for fetching the values from a, and then placing the values into the output
array. By default the order is 'C' i.e., C like indexing


```python
d = a.reshape((3, 2), order='F') # Fortran-like indexing
print(d.shape, d)
```

    (3, 2) [[0 3]
     [1 4]
     [2 5]]
    


```python
e = np.reshape(b, 6)
print(e.shape, e)

```

    (6,) [0 1 2 3 4 5]
    


```python
f = np.reshape(b, 6, order='F')
print(f.shape, f)
```

    (6,) [0 2 4 1 3 5]
    

* Ravel : Returns a contiguous falttened array. Returns a 1-D array


```python
x = np.array([[1, 2, 3], [4, 5, 6]])
print(x.shape, x)
```

    (2, 3) [[1 2 3]
     [4 5 6]]
    


```python
# flatten the array x in to one-dimension
a = x.ravel()
print(a.shape, a)

```

    (6,) [1 2 3 4 5 6]
    


```python
print(x.reshape(-1))
```

    [1 2 3 4 5 6]
    


```python
print(np.ravel(x.T)) # The T operator computes the transpose of the array x
```

    [1 4 2 5 3 6]
    

We can specify different ordering for ravel too.


```python
# different ordering modes 
print(np.ravel(x, order='F'))

```

    [1 4 2 5 3 6]
    


```python
print(np.ravel(x, order='C'))

```

    [1 2 3 4 5 6]
    


```python

print(np.ravel(x, order='K'))
```

    [1 2 3 4 5 6]
    

* Flat : Returns a 1-D iterator over the array


```python
x = np.arange(1, 7).reshape(2, 3)
print(x)
```

    [[1 2 3]
     [4 5 6]]
    


```python
# get the 1-D array of x
a = x.flat
print(type(a))
print(a[3])

```

    <class 'numpy.flatiter'>
    4
    


```python
# assignment example
x.flat = 3
print(x)

```

    [[3 3 3]
     [3 3 3]]
    


```python
x.flat[[1, 4]] = 1
print(x)
```

    [[3 1 3]
     [3 1 3]]
    

* Flatten : Returns a copy of the array collapsed into one dimension


```python
a = np.array([[1, 2], [3, 4]])
print(a)

```

    [[1 2]
     [3 4]]
    


```python
b = a.flatten()
print(type(b))
print(b)

```

    <class 'numpy.ndarray'>
    [1 2 3 4]
    


```python
c = a.flatten(order='F')
print(c)
```

    [1 3 2 4]
    

* Transpose : Computes the transpose of an array 


```python
x = np.arange(4).reshape(2, 2)
print(x)

```

    [[0 1]
     [2 3]]
    


```python
y = x.transpose()
print(y)

```

    [[0 2]
     [1 3]]
    


```python
x = np.ones((1, 2, 3))
print(x)

```

    [[[1. 1. 1.]
      [1. 1. 1.]]]
    


```python

y = np.transpose(x, (1, 0, 2))
print(y)
```

    [[[1. 1. 1.]]
    
     [[1. 1. 1.]]]
    

* Swapaxes : interchange the axes of an array


```python
x = np.array([[1, 2, 3]])
print(x)
```

    [[1 2 3]]
    


```python
y = x.swapaxes(0, 1)
print(y)

```

    [[1]
     [2]
     [3]]
    


```python
x = np.array([[[0,1],[2,3]],[[4,5],[6,7]]])
print(x)
```

    [[[0 1]
      [2 3]]
    
     [[4 5]
      [6 7]]]
    


```python
y = x.swapaxes(0, 2)
print(y)
```

    [[[0 4]
      [2 6]]
    
     [[1 5]
      [3 7]]]
    

* Creating arrays by speciying minimum dimension


```python
a = np.atleast_1d([1, 2])
print(a)
print(a.shape)

```

    [1 2]
    (2,)
    


```python
b = np.atleast_2d([1, 2])
print(b)
print(b.shape)

```

    [[1 2]]
    (1, 2)
    


```python
c = np.atleast_3d([1, 2])
print(c)
print(c.shape)
```

    [[[1]
      [2]]]
    (1, 2, 1)
    

* Expanding and squeezing the shape of arrays


```python
x = np.array([1, 2])  # x has two axis here, axis = 0 is columns and axis = 1 is row
print(x)
print(x.shape)

```

    [1 2]
    (2,)
    


```python
y = np.expand_dims(x, axis = 0)
print(y)
print(y.shape)

```

    [[1 2]]
    (1, 2)
    


```python
z = np.expand_dims(x, axis = 1)
print(z)
print(z.shape)

```

    [[[[0]
       [1]
       [2]]]]
    (1, 1, 3, 1)
    

Lets see some example for removing single-dimension entries from the shape of an array


```python
x = np.array([[[0], [1], [2]]])
print(x)
print(x.shape) # only the axis with value 1 can be squeezed

```

    [[[0]
      [1]
      [2]]]
    (1, 3, 1)
    


```python
y = np.squeeze(x)
print(y)
print(y.shape)

```

    [0 1 2]
    (3,)
    


```python
z = np.squeeze(x, axis = 0)
print(z)
print(z.shape)

```

    [[0]
     [1]
     [2]]
    (3, 1)
    


```python
z = np.squeeze(x, axis = 2)
print(z)
print(z.shape)
```

    [[0 1 2]]
    (1, 3)
    

* Splitting an array
    1. Split : Split an array into multiple sub-arrays


```python
x = np.arange(9.0)
print(x)
```

    [0. 1. 2. 3. 4. 5. 6. 7. 8.]
    


```python
# Split the array x into 3 parts
y = np.split(x, 3)
print(y)

```

    [array([0., 1., 2.]), array([3., 4., 5.]), array([6., 7., 8.])]
    


```python
# Split the array x with the split position in an 1-D array, this array must be sorted 
z = np.split(x, [2, 4, 6, 8])
print(z)

```

    [array([0., 1.]), array([2., 3.]), array([4., 5.]), array([6., 7.]), array([8.])]
    

    2. hsplit : Split an array into multiple sub-arrays horizontally i.e., column-wise


```python
x = np.arange(16.0).reshape(4, 4)
print(x)
```

    [[ 0.  1.  2.  3.]
     [ 4.  5.  6.  7.]
     [ 8.  9. 10. 11.]
     [12. 13. 14. 15.]]
    


```python
# horizontal split with at max 2 columns
y = np.hsplit(x, 2)
print(y)
```

    [array([[ 0.,  1.],
           [ 4.,  5.],
           [ 8.,  9.],
           [12., 13.]]), array([[ 2.,  3.],
           [ 6.,  7.],
           [10., 11.],
           [14., 15.]])]
    

    3. vsplit : SPlit an array into multiple sub-arrays vertically i.e., row-wise


```python
x = np.arange(16.0).reshape(4, 4)
print(x)
```

    [[ 0.  1.  2.  3.]
     [ 4.  5.  6.  7.]
     [ 8.  9. 10. 11.]
     [12. 13. 14. 15.]]
    


```python
# vertical split with two rows
y = np.vsplit(x, 2)
print(y)
```

    [array([[0., 1., 2., 3.],
           [4., 5., 6., 7.]]), array([[ 8.,  9., 10., 11.],
           [12., 13., 14., 15.]])]
    

* Adding and removing elements
    1. delete : Return a new array with sub-arrys along an axis deleted. 


```python
x = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
print(x)
```

    [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]]
    


```python
# delete first sub-array along the axis = 0 i.e., columns
y = np.delete(x, 1, 0)
print(y)

```

    [[ 1  2  3  4]
     [ 9 10 11 12]]
    


```python
# delete the second sub-array along the axis  = 1 i.e, row
z = np.delete(x, 2, 1)
print(z)
```

    [[ 1  2  4]
     [ 5  6  8]
     [ 9 10 12]]
    

    2. insert : Insert values along the given axis before the given indices


```python
a = np.array([[1, 1], [2, 2], [3, 3]])
print(a)
```

    [[1 1]
     [2 2]
     [3 3]]
    


```python
#insert 5 at positon 1, with array flatten. If axis is not given the array will be flatten first before inserting
y = np.insert(a, 1, 5)
print(y)
```

    [1 5 1 2 2 3 3]
    


```python
# insert 5 at position 1 along the row axis
z = np.insert(a, 1, 5, axis=1)
print(z)
```

    [[1 5 1]
     [2 5 2]
     [3 5 3]]
    


```python
# insert 5 at position 1 along the column axis
p = np.insert(a, 1, 5, axis=0)
print(p)
```

    [[1 1]
     [5 5]
     [2 2]
     [3 3]]
    

    3. Append : Append values to the end of an array.


```python
a = np.array([[1, 1], [2, 2], [3, 3]])
print(a)
```

    [[1 1]
     [2 2]
     [3 3]]
    


```python
# append data with the original array flattned
y = np.append(a, [[4, 4], [5, 5]])
print(y)
```

    [1 1 2 2 3 3 4 4 5 5]
    


```python
# append along the column
y = np.append(a, [[4, 4], [5, 5]], axis=0)
print(y)
```

    [[1 1]
     [2 2]
     [3 3]
     [4 4]
     [5 5]]
    

    4. resize : return a new array with the specified shape


```python
a = np.array([[0,1],[2,3]])
print(a)
```

    [[0 1]
     [2 3]]
    


```python
print(np.resize(a, (2, 3)))
```

    [[0 1 2]
     [3 0 1]]
    
