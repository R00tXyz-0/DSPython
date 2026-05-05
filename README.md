Numpy (**Num**erical **Py**thon) is an open source Python Library that’s widely used in science and engineering. The Numpy Library contadins multidimensional array data structures, such as the homogeneous, N-dimensional `ndarray`, and a large library of functions that operate efficiently on these data structures.

## ***Why Use Numpy :***
Python lists are excellent, general-purpose containers. They can be “heterogeneous”, meaning that they can contain elements of a variety of types, and they are *quite fast when used to perform individual operations on a handful of elements*.

Depending on the characteristics of the data and the types of operations that need to be performed, other containers May be more appropriate; by exploiting these characteristics, we can ***improve speed***, *reduce memory consumption*, and *offer a high-level syntax* *for performing a variety of common processing tasks*. NumPy shines when there are *large quantities of “homogeneous” (same-type) data* to be processed on the CPU.

## ***Numpy array restrictions :***
- All elements of the array must be of the same type of data.
- Once created, the total size of the array can’t change.
- The shape must be “rectangular”, not “jagged”; e.g., each row of a two-dimensional array must have the same number of columns.

## ***Use Numpy :***

+ Import NumPy : 

```python
>>> import numpy as np
```

+ Exemple : 

```Python
>>> a = np.array([[2, 5, 5]
			  [5, 8, 9]
			  [8, 7, 3]])  
```

+  Some NumPy attributs (Basics) :

`ndim` : *the number of dimensions of the array*

```python
>>> np.ndim
3
```
		
`shape` : *Size of the array in each dimension*

```Python
>>> np.shape
(3, 3)
```

`dtype` : *the data type of element stored in the array*

```python
>>> np.dtype
dtype('int64')
```

`size` : *the fixed, totale number of elements in the array*

```Python
>>> np.size
9
```

*Example of how `size` is builded :*

```Python
>>> import math
>>> np.size = math.prod(a.shape)
True
```

+ ###  How to create a basic array using some functions : 

`zeros` : *Create an array filled with 0 .*
`ones` : *Create an array filled with 0 .*

```Python
>>> a = np.zeros((2, 3))
>>> a2 = np.ones((2, 3))
>>> print(a)
>>> print(a2)
```

- Output : 

```Python
[[0. 0. 0.]
 [0. 0. 0.]]
 
 [[1. 1. 1.] 
 [1. 1. 1.]]
```

+ *Specifying the data type* : 

```Python
>>> a2 = np.ones((2, dtype=np.int64))
>>> print(a2)

Output : 
array([1, 1])
```

	

`eye` : *Create an identity array ***( diagonal = 1, rest = 0 )***

```Python
>>> a = np.eye(3)
>>> print(a)
 
Output :

[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

`full` : *Create an array filled with specific values*

```Python
>>> a = np.full((2, 4), 9)
>>> print(a)
 
Output :

[[9 9 9 9] 
 [9 9 9 9] 
 [9 9 9 9]]
```

`empty` : *Create an array whose initial content is random and dépends on the state of the memory.*

```Python
>>> a = np.empty(2)
>>> print(a)
```

- Output : 

```Python
(array([1.58911749e-315, 0.00000000e+000, 4.94065646e-324, 6.88311723e-310]),)
```

`arange` : *Create an array with a range of elements.*

```Python
>>> py = np.arange(5)

# Output : 
array([0, 1, 2, 3, 4])
```

- *to sepcify the array :*

```Python
# Exemple :
>>>  np.arange(d d,First Num, Last Num, Step size)
>>> py = np.arange(5, 15, 3)
>>> print(py)
# Output : 
array([5, 8, 11, 14])
```


`linespace` : *create an array with values that are spaced linearly in a specified interval*

```Python
>>> py = np.linespace(0, 6, 3), 
>>> py1 = np.linespace(0, 10, 5)
>>> print(py)
>>> print(py2)

# Output :
array([ 0. ,  3,  6. ])
array([ 0. ,  2.5,  5. ,  7.5, 10. ])
```

+ ### Adding, removing, and sorting elements : 

```Python
# the Main Exepmle : 
>>> arr = np.array([2, 1, 5, 3, 7, 4, 6, 8])
```

+ Adding and Removing an element : 

`append` : *Add an elements in the array or an array*
`delete` : *remove an element or an array from an array*

`unique` : *it remove duplicate and rerturn a sorted array*
`insert` : *inserts a value (or values) into an array at a specified index.*


```Python

>>> a = np.append(arr, 9)
>>> print(a)
>>> arr2 = np.array(arr, [7, 1])
>>> a2 = np.append(arr, arr2)
>>> print(arr2)
>>> a3 = np.delete(arr, 2)
>>> print(a3)
>>> a4 =  np.delete(arr, [4, 6])
>>> print(a4)

# Inser and Delete using indice :
>>> a5 = np.insert(arr, 5, 100)
>>> np.delete(arr, indice, axis) # just an exepmle (Remove a line)
>>> py1 = np.array([1, 2, 2, 4 , 6])
>>> pyC = np.unique(py1)
>>> print(PyC)

#Output : 
[2, 1, 5, 3, 7, 4, 6, 8, 9]
[2, 1, 5, 3, 7, 4, 6, 8, 7, 1]
[1, 5, 3, 7, 4, 6, 8, 7, 1]
[2, 1, 5, 3, 7, 8, 7, 1]
[1, 2, 4 ,6]

```
+ sorting array elements :

```Python  
>>> b = np.sort(arr)  
>>> print(b)

# Output : 
[1 2 3 4 5 6 7 8]
```

+ *For more about using Sort Functions :* [numpy Sort](https://numpy.org/doc/stable/reference/generated/numpy.sort.html#numpy.sort)

`concatenate` : concatenate arrays

```Python
>>> py1 = np.array([1, 2, 2, 4, 6])
>>> py2 = np.array([4,6,9])
>>> pyR = np.concatenate(py1, py2)

# Output :
array[(1, 2, 2, 4, 6, 4, 6, 9)]
```


+ ### Les Fonctions Statistiques : 
 
+ the main array : 

```Python
a = np.array([1, 9, 78, 0.5, 3])
```

`mean` : *Calculates the arithmetic average of the array elements*

``` Python
>>> py = np.mean(a) 
>>> print(py)
>>> py1 = np.sum(a)
>>> print(py1)
>>> py2 = np.min(a)
>>> print(py2)
>>> py3 = np.max(a)
>>> print(py3)
>>> py4 = np.std(a) # écart-type
>>> print(py4)
>>> py5 = np.var(a) # Variance
>>> print(py5)

# Output

py = 18.3
py1 = 91.5
py2 = 0.5
py3 = 78
py4 = 30.002666548158683
py5 = 900.1600000000001


