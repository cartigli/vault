how to work with scalars, vectors, and matrices
	the answer is [arrays] - numpy's bread n' butter
```python
import numpy as np

# declaring scalars, vectors, and matrices

# scalars # is this not just declaring a variable :/
s = 5 # int / float

# vectors
v = np.array([5,-2,4])
#print(v) # [ 5 -2 4]
# by default, 'v' is a row vector
# all v's or just new single dimension matrices?

# matrices
m = np.array([[5,12,6],[-3,0,14]]) # two vectors
print(m) #[[ 5 12  6]
#          [-3  0 14]]

# type() returns the type of variable given as arg
#print(type(m)) # <class 'numpy.ndarray'>
#print(type(v)) # <class 'numpy.ndarray'>
#print(type(s)) # <class 'int'>
# ' nd ' in ndarray stands for _n dimensions {{ to be defined by you! }}
# m is 2 dimensions, v is 1

# if you wanted cohesion across variable types, you could unify them:
s_ = np.array(5)
# print(type(s_)) # <class 'numpy.ndarray'> ; still a scalar

# data shapes
# .shape() returns the dimensions ; ([2,3]) for m , (3,) for v & () for s_ 
#print(s_.shape)

# if we want to change an array's shape :
# v is the shape (3,) but we know how dramatic python is + we made v
# its shape is (3,1) so if we want to reshape it, we can . . .
#      v.reshape(1,3) makes v into:
#			[[ 5 -2 4]] ; a row vector
#		v.reshape(3,1) makes v into:
#			[[ 5]
#            [-2]
#            [ 4]] # a column vector#
# you basically choose the configuration of the pre-existing dimensions
# data is unaffected
print(v.reshape(1,3))
print(v.reshape(3,1))