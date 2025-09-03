```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

print('\n','Take this vector, for example. It runs from 0 to it\'s position: [ 7 , 3 ]. A vector\'s direction is determined by its values.','\n')

x_beg, y_beg = 0, 0
u, v = 7, 3

w, z = -7, -3

a, b = -2, 4


fig, ax = plt.subplots()

# plot vector using quiver
ax.quiver(x_beg, y_beg, u, v, angles='xy', scale_units='xy', scale=1, color='red', label='Vector')

# set plot & aspect ration
ax.set_xlim(-10,10)
ax.set_ylim(-10,10)
ax.set_aspect('equal')

ax.set_title('2D space')
ax.legend()
ax.grid(True)

plt.show()
plt.close()


print('\n','Imagine we moved the vector to the opposite direction. This, shown in blue, is the vector [ -7, -3 ]. It is equal to the original vector *[-1].','\n')


fig, ax = plt.subplots()


ax.quiver(x_beg, y_beg, u, v, angles='xy', scale_units='xy', scale=1, color='red', label='Vector')

ax.quiver(w_beg, z_beg, w, z, angles='xy', scale_units='xy', scale=1, color='blue', label='-Vector')

# set plot & aspect ration
ax.set_xlim(-10,10)
ax.set_ylim(-10,10)
ax.set_aspect('equal')

ax.set_title('2D space; polars visualized')
ax.legend()
ax.grid(True)

plt.show()
plt.close()

print('For clarity, a vector of [ -2, 4 ] would be positioned here, as seen with the purple vector.','\n')

fig, ax = plt.subplots()


ax.quiver(x_beg, y_beg, u, v, angles='xy', scale_units='xy', scale=1, color='red', label='Vector')

ax.quiver(x_beg, y_beg, w, z, angles='xy', scale_units='xy', scale=1, color='blue', label='-Vector')

ax.quiver(x_beg, y_beg, a, b, angles='xy', scale_units='xy', scale=1, color='blue', label='-Vector')

# set plot & aspect ration
ax.set_xlim(-10,10)
ax.set_ylim(-10,10)
ax.set_aspect('equal')

ax.set_title('2D space; 3 Vectors')
ax.legend()
ax.grid(True)

plt.show()
plt.close()


# get to the point
print('This space is defined by its vectors. If we remove them, it would be an empty space, but consider two vectors: [ 1, 0 ] & [ 0, 1 ]. Together, these vectors form a matrix:','\n','[ 1 , 0 ]','\n','[ 0 , 1 ]','\n','This is the fundemantel definition of the 2D space, shown below:','\n')

fig, ax = plt.subplots()

n, m = 1, 0
l, o = 0, 1

ax.quiver(x_beg, y_beg, n, m, angles='xy', scale_units='xy', scale=1, color='blue', label='Vector [ 1 , 0 ]')

ax.quiver(w_beg, z_beg, l, o, angles='xy', scale_units='xy', scale=1, color='red', label='Vector [ 0 , 1 ]')

# set plot & aspect ration
ax.set_xlim(-10,10)
ax.set_ylim(-10,10)
ax.set_aspect('equal')

ax.set_title('Fundamental definition of 2D plane')
ax.legend()
ax.grid(True)

plt.show()
plt.close()