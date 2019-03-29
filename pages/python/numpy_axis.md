---
layout: page
title: Numpy Axis
---

#### Axis in Numpy

If `b` has shape `(6,7,8,9)` and we `np.mean(b, axis=2)`, then the axis 2 (dimension with size 8) is collapsed. The result has shape `(6,7,9)`. In other words, `mean` is applied across axis 2. 

If `b` is a 2D matrix, axis 0 is the first dimension (the "rows") and axis 1 is the second dimension (the "columns"). In this case, `np.mean(b, axis=0)` applies `mean` across rows of `b` and rows are collapsed.


```
a = [[1,2],[10,11]]
b = [[3,4],[12,13]]
c = [[5,6],[14,15]]

>>> np.mean((a,b,c))
8.0

>>> np.mean((a,b,c), axis=0)
array([[ 3.,  4.],
       [12., 13.]])

>>> np.mean((a,b,c), axis=1)
array([[ 5.5,  6.5],
       [ 7.5,  8.5],
       [ 9.5, 10.5]])

>>> np.mean((a,b,c), axis=2)
array([[ 1.5, 10.5],
       [ 3.5, 12.5],
       [ 5.5, 14.5]])
```

_Note: A tuple of lists is treated the same as a list of lists._

```
d = [a,b,c]

def mn(*args):
	return np.mean(args, axis=0)

# This is the same as np.mean(d, axis=0)
>>> mn(*d)
array([[ 3.,  4.],
       [12., 13.]])
```