```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn

print('\n','Take this scalar, for example. It\'s position is [ 7 , 3 ].','\n')

x = 7
y = 3
plt.scatter(x,y)
plt.title('[7,3]')
plt.show()
plt.close()

print('\n','Imagine we wanted to move the scalar, or point, to another spot:','\n')
