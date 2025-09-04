```python
# 1. Force an interactive backend
import matplotlib
matplotlib.use('Qt5Agg')

# 2. Import other libraries as usual
import matplotlib.pyplot as plt
import numpy as np
from mpl_toolkits.mplot3d import Axes3D

# Create a figure and a 3D Axes
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(projection='3d')

# Generate the data
x = np.arange(-5, 5, 0.25)
y = np.arange(-5, 5, 0.25)

# Create some Z data and call a plotting function
z = np.sin(x) + np.cos(y) # Example Z data
ax.scatter(x, y, z, c='r', marker='o') # Tells matplotlib WHAT to draw

# Add some labels for context
ax.set_xlabel('X Axis')
ax.set_ylabel('Y Axis')
ax.set_zlabel('Z Axis')

# Now, show the plot
plt.show()
plt.close
```

```python
plt.show()
plt.close()