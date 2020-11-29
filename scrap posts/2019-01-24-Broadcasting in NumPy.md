---
title: 	"Broadcasting in NumPy"
date: 	2019-01-24
mathjax: True
tags: 	[machine_learning]
---

# Broadcasting in NumPy
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
The line ```y = x + v``` works even though x has shape(4, 3) and v has shape (3,) due to broadcasting; this line works as if v actually had shape (4, 3), where each row was a copy of v, and the sum was performed elementwise.  

Broadcasting two arrays together follows these rules:  
1. If the array do not have the same rank, prepend the shape of the lower rank array with 1's until both shapes have the same length.
2. The two arrays are said to be compatible in a dimension if they have the same size in the dimension, or if one of the arrays has size 1 in that dimension.
3. The arrays can be broadcast together if they are compatible in all dimensions.
4. After broadcasting, each arrays behaves as if it had shape equal to the elementwise maximum of shapes of the two input array.
5. In any dimension where one array had size 1 and the other array had size greater than 1, the first array behaves as if it were copied along that dimension.

Function that support braodcasting are known as **universal funcions**. The full list of universal functions is available [here](https://docs.scipy.org/doc/numpy/reference/ufuncs.html#available-ufuncs)




