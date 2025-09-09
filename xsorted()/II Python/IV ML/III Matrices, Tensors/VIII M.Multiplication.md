let's get it
[ scalars ]
	1 x 2 = 2
	4 x {-4} = 16

[ vectors ]
	same as usual, must be same length
$$\begin{bmatrix}
2 \\
3 \\
-1
\end{bmatrix} \cdot \begin{bmatrix}
3 \\
0 \\
5
\end{bmatrix} = \begin{bmatrix}
{2 * 3 + 3*0 + -1*5}
\end{bmatrix} = \begin{bmatrix}
1
\end{bmatrix} {\text{; a scalar !}}$$
		Dot Product ^
			the sum of the products of the corresponding elements
numpy got a .dot() method :)

```python
import numpy as np

v=np.array([3,7,-8])
v_ = np.array([6,0,29])
print(np.dot(v,v_))
```

we get:```-214```
	the scalar
		this also is silly ; does it infer there is dot division?

```python
import numpy as np

v = np.array([3,7,-8])
v_ = np.array([6,0,29])

x = np.array([2,-7,0])
x_ = np.array([5,3,19])

vv=np.array([v,v_])
xx=np.array([x,x_])

print(np.dot(vv,xx))
```
HAHAH ok wait this threw an error lets fix it
```python
import numpy as np

v = np.array([3,7,-8])
v_ = np.array([6,0,29])

x = np.array([2,-7,0])
x_ = np.array([5,3,19])

vv=np.array([v,v_])
xx=np.array([x,x_])

xx = xx.T

print(np.dot(vv,xx))
```
ba da freaking boom 

matrices need to be coordinated, not the same size at all
this first try didn't work because we tried to multiply 2x3 by 2x3
	I think of it like they need a dimension to coordinate over and commune between
	When we transposed xx, the equation became 2x3 by 3x2, which fixed the error
		We didn't remove or alter any of the data within xx and it remains in the same orientation internally
		print(vv.shape, xx.shape)

```python
import numpy as np

v = np.array([3,7,-8])
v_ = np.array([6,0,29])
print('v & v_ shapes:',v.shape,v_.shape)

x = np.array([2,-7,0])
x_ = np.array([5,3,19])
print('\nx & x_ shapes:',x.shape,x_.shape)

vv=np.array([v,v_])
xx=np.array([x,x_])
print('\nvv & xx shapes:',vv.shape,xx.shape)

xx = xx.T

vx = np.dot(vv,xx)

print('\ndot prod:',vx)

print('\nresulting shape:',vx.shape)
```

```
v & v_ shapes: (3,) (3,)
x & x_ shapes: (3,) (3,)
vv & xx shapes: (2, 3) (2, 3)
dot prod: [[ -43 -116]
 [  12  581]]
resulting shape: (2, 2)
```
dimensions of the results form the dot product are as so:
	if we multiply a 2x3 matrix by a 3x2 matrix, they meet over the 3 common ground and collapse over it to be 2x2
		3x12 matrix by a 12 x 46 matrix has a dot product of 3x46 shape
```python
import numpy as np

v = np.array([3,7,-8])
v_ = np.array([6,0,29])

x = np.array([2,-7,0])
x_ = np.array([5,3,19])

vv=np.array([v,v_]) # 2 x 3
xx=np.array([x,x_]) # 2 x 3
print('\n\nvv shape:',vv.shape)
print('\nxx shape:',xx.shape)

vv = vv.T # 3 x 2
print('\nvv.T shape:',vv.shape)

xv = np.dot(xx,vv) # bless

#print(np.dot(vv,xx))
#print(np.dot(xx,vv)) # ( 3 x 2 } x { 2 x 3 }

print('\n\n',xv.shape)
print(xv)
```
no change
		*its just the sum of one of the dimensions of each matrix*

xx * vv.T = [ [ -43,   12 ]
                     [ -116,   581 ] ]

vv * xx.T = [ [ -43,  -116 ]
                     [    12,  581 ] ]

that's actually pretty cool, let's try something
```python
import numpy as np
v=np.array([[-43,-116],[12,581]])
print('\n\nv stats:',v.shape,'\n',v)
v = v.T
print('\n\nv.T stats:',v.shape,'\n',v)
```
well i'll be bob's uncle
```
v stats: (2, 2) 
 [[ -43 -116]
 [  12  581]]
v.T stats: (2, 2) 
 [[ -43   12]
 [-116  581]]
```
so, 
$$vv \cdot xx.T = (xx \cdot vv.T).T$$
convenient and interesting.