vectors
we've seen rows and columns ; and movement between
```python
import numpy as np
v=np.array([1,2,3])
v_=np.array([1,2,3])
print('v_ shape:',v_.shape,'v shape:',v.shape)
print('v_:',v_,'v:',v)

v_ = v_.reshape(1,3)

print('v_ shape:',v_.shape,'v shape:',v.shape)

print('v_:',v_,'v:',v)
```
data does not change, but shape can
this was a manual transposition
for the situation above, $v = v-^T$
		{{ ^ my b ; the matrix v is equal to v_ transposed }}
			the row vector v became the column vector v_
				a vector transposed twice is the original vector

[ Transposing ] a matrix
	M x N matrix transposed is an N x M matrix
$$\begin{bmatrix}
5 & 7 & 9 \\
2 & 3 & 4
\end{bmatrix}^T = \begin{bmatrix}
5 & 2 \\
7 & 3 \\
9 & 4
\end{bmatrix}$$
in code
```python
import numpy as np
v=np.array([1,2,3])
v_=np.array([1,2,3])
vv=np.array([v,v_])
print('vv info:',vv.shape,'\n',vv)
vv = vv.T # transpose
print('vv.T info:',vv.shape,'\n',vv)
```
prod:
```
vv info: (2, 3) 
 [[1 2 3]
 [1 2 3]]

vv.T info: (3, 2) 
 [[1 1]
 [2 2]
 [3 3]]
```
bada bing, bada boom

dot prod: [[ -43 -116]
 [  12  581]]