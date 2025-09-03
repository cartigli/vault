```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

print('\n','Take this vector, for example. It runs from 0 to it\'s position: [ 4 , 1.5 ]. A vector\'s direction is determined by its values.')

x_beg, y_beg = 0, 0
u, v = 4, 1.5

w, z = -4, -1.5

a, b = -2, 3.5


fig, ax = plt.subplots()

# plot vector using quiver
ax.quiver(x_beg, y_beg, u, v, angles='xy', scale_units='xy', scale=1, color='red', label='Vector')

# set plot & aspect ration
ax.set_xlim(-5,5)
ax.set_ylim(-5,5)
ax.set_aspect('equal')

ax.set_title('2D space')
ax.legend()
ax.grid(True)

plt.show()
plt.close()


print('\n\n\n','Imagine we moved the vector to the opposite direction. This, shown in blue, is the vector [ -4, -1.5 ]. It is equal to the original vector *[-1].')


fig, ax = plt.subplots()


ax.quiver(x_beg, y_beg, u, v, angles='xy', scale_units='xy', scale=1, color='red', label='Vector I')

ax.quiver(x_beg, y_beg, w, z, angles='xy', scale_units='xy', scale=1, color='blue', label='-Vector I')

# set plot & aspect ration
ax.set_xlim(-5,5)
ax.set_ylim(-5,5)
ax.set_aspect('equal')

ax.set_title('2D space; Opposing vectors visualized')
ax.legend()
ax.grid(True)

plt.show()
plt.close()

print('\n\n\n','For clarity, a vector of [ -2, 3.5 ] would be positioned here, as seen with the green vector.')

fig, ax = plt.subplots()


ax.quiver(x_beg, y_beg, u, v, angles='xy', scale_units='xy', scale=1, color='red', label='Vector I')

ax.quiver(x_beg, y_beg, w, z, angles='xy', scale_units='xy', scale=1, color='blue', label='-Vector I')

ax.quiver(x_beg, y_beg, a, b, angles='xy', scale_units='xy', scale=1, color='green', label='Vector II')

# set plot & aspect ration
ax.set_xlim(-5,5)
ax.set_ylim(-5,5)
ax.set_aspect('equal')

ax.set_title('2D space; 3 Vectors')
ax.legend()
ax.grid(True)

plt.show()
plt.close()


# get to the point
print('\n\n\n','This space is defined by its vectors. If we remove them, it would be an empty space, but consider two vectors: [ 1, 0 ] & [ 0, 1 ]. Together, these vectors form a matrix:','\n','[ 1 , 0 ]','\n','[ 0 , 1 ]','\n','This is the fundamental definition of the 2D space, shown below:')

fig, ax = plt.subplots()

n, m = 1, 0
l, o = 0, 1

ax.quiver(x_beg, y_beg, n, m, angles='xy', scale_units='xy', scale=1, color='red', label='Vector [ 1 , 0 ]')

ax.quiver(x_beg, y_beg, l, o, angles='xy', scale_units='xy', scale=1, color='blue', label='Vector [ 0 , 1 ]')

# set plot & aspect ration
ax.set_xlim(-2,2)
ax.set_ylim(-2,2)
ax.set_aspect('equal')

ax.set_title('Fundamental definition of 2D plane')
ax.legend()
ax.grid(False)

plt.show()
plt.close()