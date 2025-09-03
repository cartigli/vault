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
 \end{bmatrix} = \begin{bmatrix}
 2*8 + 7*1 + 5*0 & 2*2 + 7*-15 + 5*5\\
  -3*8 + 4*1 + .5*0 & -3*2 + 4*-15 + .5*5
 \end{bmatrix} = $$
$$=\begin{bmatrix}
 16+7+0 & 4+(-105)+25 \\
 -24+4+0 & -6+(-60)+2.5
 \end{bmatrix}= \begin{bmatrix}
 23 & -76 \\
 -20 & 63.5
 \end{bmatrix}$$