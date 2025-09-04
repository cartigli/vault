you can multiply matrices by scalars
```python
import numpy as np

v=np.array([[6,40,-33],[77,2,0]])
s=222
x=v*s
print(x)
```
$$\begin{bmatrix}
 2 & 7 & 5 \\
 -3 & 4 & .5
 \end{bmatrix} \cdot \begin{bmatrix}
 8 & 2 \\
 1 & -15 \\
 0 & 5
 \end{bmatrix} = $$$$=\begin{bmatrix}
 2*8 + 7*1 + 5*0 & 2*2 + 7*-15 + 5*5\\
  -3*8 + 4*1 + .5*0 & -3*2 + 4*-15 + .5*5
 \end{bmatrix}$$
$$=\begin{bmatrix}
 16+7+0 & 4+(-105)+25 \\
 -24+4+0 & -6+(-60)+2.5
 \end{bmatrix}$$
 
  $$=\begin{bmatrix}
 23 & -76 \\
 -20 & 63.5
 \end{bmatrix}$$
 *in code*
```python
import numpy as np

v=np.array([[2,7,5],[-3,4,0.5]])
v_=np.array([[8,1,0],[2,-15,5]])
v_ = v_.T
print('factors\' shape:',v.shape,v_.shape) # 2x3 by 3x2
vv = np.dot(v,v_)
print('\nvv:\n',vv)

print(' ')

v_ = v_.T # transposed twice, so original shape
v=v.T
print('factor\'s shape:',v.shape,v_.shape) # 3x2 by 2x3
vv = np.dot(v,v_)
print('\nvv:\n',vv)
```

the factors collapse over their related dimension and take the shape of the remaining dimension
		mxk by kxn = mxn

$$\begin{bmatrix}
 \text{[ 2, 7, 5, ]} \\
 \text{[ -3, 4, .5 ]}
 \end{bmatrix} \cdot \begin{bmatrix}
 \text{[ 8, 1, 0 ]}\\
 \text{[ 2, -15, 5 ]}
 \end{bmatrix}.T$$
	*its always row vector times column vector ; the row vector [ 2, 7, 5 ] is multiplied by the column vector [ 8, 1, 0 ] - it is a column vector after the transpoition*