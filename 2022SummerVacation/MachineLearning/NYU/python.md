# python

## Lecture Two

- `np.linspace()`
- `np.random.normal()`
- `np.vstack()`
- `ndarray.reshape(-1, ?)`
- `np.matmul()`
- `np.sum()`
- `np.ones((?,))`
- `plt.semilogy()`
  - zeros ... whey the column part of size is empty?
- `np.arange()`

### `np.linspace()`

Returns number spaced evenly.

syntax

```python
numpy.linspace(
    start,
    stop,
    num = 50,
    endpoint = True,
    retstep = False,
    dtype = None
)
```

- `start`: array_like
  - start of interval range, by default `start=0`
- `stop`: array_like
  - end of interval range
- `retstep`: bool, optional
  - if `True`, returns `(samples, step)`. By default `retstep = False`
- `num`: int, optional
  - number of samples to generate
- `dtype`: dtype, optional
  - type of output array

return

```python
ndarray
step: [float, optional] if retstep = True
```

example

```python
x = np.linspace(0, 2, 6)
x: array([0. , 0.4, 0.8, 1.2, 1.6, 2. ])
```

### `np.random.normal()`

Draw random samples from a normal (Gaussian) distribution.

syntax

```python
numpy.random.normal(
    loc=0.0,
    scale=1.0,
    size=None
)
```

- `loc`: float or array_like floats
  - center of the distribution
- `scale`: float or array_like of floats
  - standard deviation (spread or "width") of the distribution
- `size`: int or tuple of ints, optional
  - output shape. If the given shape is, e.g., `(m, n, k)`, then `m * n * k` samples are drawn. If size is `None` (default), a single value is returned a single value is returned if `loc` and `scale` are both scalars. Otherwise, `np.broadcast(loc, scale).size` samples are drawn

return

```python
ndarray or scalar
```

### `np.vstack()`

used to stack the sequence of input arrays vertically to make a single array.

syntax

```python
numpy.vstack(tup)
```

- `tup`: sequence of ndarrays
  - The arrays must have the same shape along all but the first axis. 1-D array must have the same length

return

```python
stacked: ndarray
```

example

```python
a = np.array([1, 2, 3])
a = np.array([4, 5, 6])
np.vstack((a, b))
# array([[1, 2, 3],
#        [4, 5, 6]])
```

### `ndarray.reshape()` / `numpy.reshape()`

syntax

```python
numpy.reshape(a, newshape, order='C')
```

- `a`: array_like
  - array to be reshaped
- `newshape`: int or tuple of ints
  - the new shape should be compatible with the original shape.
  - one shape dimension can be **-1**. In this case, the value is inferred from the length of the array and remaining dimensions
- order: $ \dots $

return

```python
reshaped_array: ndarray
```

example

```python
a = np.arange(6).reshape((3, 2))
# array([[0, 1],
#       [2, 3],
#       [4, 5]])

a = np.array([
    [1, 3, 3], 
    [4, 5, 6]
    ])

a.reshape((3, -1)) # the unspecified value is inferred to be 2
# array([[1, 2],
#        [3, 4],
#        [5, 6]])
```

### `np.matmul()`

Matrix product of two arrays

The behavior depends on the arguments in the following way.

- If both arguments are 2-D they are multiplied like conventional matrices.
- If either argument is N-D, N > 2, it is treated as a stack of matrices residing in the last two indexes and broadcast accordingly.
- If the first argument is 1-D, it is promoted to a matrix by prepending a 1 to its dimensions. After matrix multiplication the prepended 1 is removed.
- If the second argument is 1-D, it is promoted to a matrix by appending a 1 to its dimensions. After matrix multiplication the appended 1 is removed.

`matmul` differs from dot in two important ways:

- Multiplication by scalars is not allowed, use * instead.
- Stacks of matrices are broadcast together as if the matrices were elements, respecting the signature (n,k),(k,m)->(n,m):

### `numpy.sum()`

return sum of array elements over a given axis

syntax

```python
numpy.sum(
    arr,
    axis,
    dtype,
    out
)
```

- `arr`: array_like
  - elements to sum
- `axis`: None or int or tuple of ints, optional
  - axis or axes along which sum is performed. The default value is `axis=None`
- `dtype` dtype, optional
- `out`: ndarray, optional
  - alternative output array in which to place the result. It must have the same shape as the expected output

return

```python
sum_along_axis: ndarray
```

example

```python
np.sum([0.5, 1.5])
# 2.0

np.sum([0.5, 0.7, 0.2, 1.5], dtype=np.int32)
# 1

np.sum([[0, 1], [0, 5]])
# 6

np.sum([[0, 1], [0, 5]], axis=0)
# array([0, 6])

np.sum([[0, 1], [0, 5]], axis=1)
# array([1, 5])
```

### `numpy.ones(?,)`

Notice the difference

```python
numpy.ones(4,)
# array([1., 1., 1., 1.,])
numpy.ones(4,).shape()
# (4,)
numpy.ones(1, 4)
# array([[1., 1., 1., 1.,]])
numpy.ones(1, 4).shape()
# (1,4)
```

a regular python 1-D array have a shape `(?,)`, where `?` is the length of the array

### `matplotlib.pyplot.semilogy`

this is just a thin wrapper around `plot` which additionally changes the `y-axis` to log scaling.

## Lecture Three

- `np.meshgrid`
- `np.arange`

### `np.meshgrid`

Return coordinate matrices from coordinate vectors.

Make N-D coordinate arrays for vectorized evaluations of N-D scalar/vector fields over N-D grids, given one-dimensional coordinate arrays `x1, x2, ..., x3`

#### Example

```python
x1 = np.linspace(1, 5, 5)
x2 = np.linspace(21, 25, 5)

xx1, xx2 = np.meshgrid(x1, x2)
xx1.shape, xx2.shape
# ((5, 5), (5, 5))
```

```python
>>> xx1
array([[1., 2., 3., 4., 5.],
       [1., 2., 3., 4., 5.],
       [1., 2., 3., 4., 5.],
       [1., 2., 3., 4., 5.],
       [1., 2., 3., 4., 5.]])
>>> xx2
array([[21., 21., 21., 21., 21.],
       [22., 22., 22., 22., 22.],
       [23., 23., 23., 23., 23.],
       [24., 24., 24., 24., 24.],
       [25., 25., 25., 25., 25.]])
```

### `np.arange`

Return evenly spaced values within a given interval.

syntax

```python
numpy.arange(
  [start,]
  stop,
  [step,]
   )
```

- `start`: integer or real
  - Start of interval. The default is 0.
- `stop`: integer or real
  - End of interval. The interval does not include this value.
- `step`: integer or real
  - Spacing between values.

Return

```python
arange : ndarray
```

