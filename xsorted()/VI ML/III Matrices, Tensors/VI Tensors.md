scalars, vectors, and matrices are all [tensors]
$$\begin{bmatrix}
5
\end{bmatrix} = \text{Tensor 1 x 1 | rank: 0}$$
$$\begin{bmatrix}
6 & 7
\end{bmatrix} = \text{Tensor m x 1 | rank: 1}$$
$$\begin{bmatrix}
5 & 6 \\
3 & 4
\end{bmatrix} = \text{Tensor m x n [ 2 x 2 ] | rank: 2 }$$
$$? = \text{Tensor k x m x n}$$

hold on to your seats, folks. A tensor can be dimensions k x m x n , but it is not different from an ndarray in coding terms and follows the same pattern we've seen so far : a line is many scalars, a plane is many lines, and guess what, the next dimension is many planes
		the pattern is the previous dimension must be built on to proceed
```python
import numpy as np

# gotta build, right? so we'll use two matrices to make a tensor
m = np.array([[2,5,1],[7,3,6]])
print('\n','m\'s shape:',m.shape,'\n\n')

m_ = np.array([[7,9,8],[5,20,7]])
print('\n','m_\'s shape',m_.shape,'\n\n') 
#m's shape: (2, 3)
#m_'s shape (2, 3)
# they both have the same shape of 2 rows and 3 columns

# im ngl this is clean
t = np.array([m,m_])
print('\n','t:',t)
# [[[ 2 5 1] 
#   [ 7 3 6]]
#
#  [[ 7 9 8]
#   [ 5 20 7]]]
# they freaking printed out the three 3 object , big stuff, huge things

print('\n','t shape:',t.shape) # (2, 2, 3) this is great : t is the shape of 2 matrices which are 2 by 3 each
# matrices on matrices

# it's also not like we couldn't do this manually or adding two preexisting matrices is the only method - just gets tedious + fat
# I actually wish they had showed this first but whatever still cool
t_ = np.array([[[2,5,1],[7,3,6]],[[7,9,8],[5,20,7]]]) # 2 x 2 x 3
print('\n\n','t_:',t_)
print('\n','t_ shape:',t_.shape)