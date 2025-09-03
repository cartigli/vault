we can add and subtract:
 they must have the same dimensions:$$\begin{bmatrix}
 2 & 7 & 5 \\
 -3 & 4 & .5
 \end{bmatrix} + \begin{bmatrix}
 8 & 2 & 1 \\
 -15 & 0 & 5
 \end{bmatrix} = \begin{bmatrix}
 2+8 & 7+2 & 5+1 \\
 (-3)+(-15) & 4+0 & .5+5
 \end{bmatrix} = \begin{bmatrix}
 10 & 9 & 6 \\
 -18 & 4 & 5.5
 \end{bmatrix}$$
	 each were a 2 x 3 matrix, results in a 2x3 matrix
	
even easier in python:
```python
import numpy as np
m = np.array([[2,5,1],[7,3,6]])
m_ = np.array([[7,9,8],[5,20,7]])
mm = m + m_
print(mm) 
```

vectors are just one dimensional matrices, so 
		they work the same way 
		and are bound by the same rules
			they need to be the same size, or since it is vectors, its length
```python
import numpy as np
v = np.array([1,2,3,4,5])
v_ = np.array([5,4,3,2,1])
vv = v + v_
v_v = v - v_
v2 = v * v_
v1 = v / v_
print('vv:',vv,'\n','v_v:',v_v,'\n','v2:',v2,'\n','v1:',v1)
```
all remained the same shape
```
vv: [6 6 6 6 6] 
 v_v: [-4 -2  0  2  4] 
 v2: [5 8 9 8 5] 
 v1: [0.2 0.5 1.  2.  5. ]
```

```python
import numpy as np
v=([1,2,3,4,5])
v_=([5,4,3,2,1])
vv=np.array([v,v_])
print('\n\n','vv shape:',vv.shape,'\n')
print('\n','vv:',vv)
```

```
vv shape: (2, 5) 
vv: [[1 2 3 4 5] [5 4 3 2 1]]
```
there you go ladies and gentlemen, a matrix made out of 2 vectors

something to keep you up at night is this fun bonus
adding vectors or matrices of different sizes is impossible. Its mathemtically and programatically impossible and makes no computational sense. it will return an error. Except...
Adding Scalars to Matrices
```python
import numpy as np
v=np.array([4,1,7,3,2])
v_=np.array([0,-4,2,6,7])
m=np.array([v,v_])
print('m shape:',m.shape,' & m:',m,'\n\n')

m = m + 2
print('m after adding 2 shape:',m.shape,' & m after adding freaking 2:',m,'\n\n')
```

```
m shape: (2, 5)  & m: [[ 4  1  7  3  2]
                       [ 0 -4  2  6  7]] 
m after 2 shape: (2, 5)  & m after adding freaking 2: [[ 6  3  9  5  4]
                                                       [ 2 -2  4  8  9]] 
 ```
 every value got +2 
 i find this absurd but also straightforward. This kind of straight forward is either 1/1,000,000 or going to come back to bite later. Paranoia.
		 dude said it has no algebraic meaning 
			 heard that