```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

from mpl_toolkits.mplot3d import Axes3d # 3D grahs, let's go | outdated
	generate data to train on
	create targets to aim for 
	plot the training data

generate training data ; linear relationship within
```python
observations = 10000 # n
```
2 variable linear model ; x & z

{ np.random.uniform (low,high, size) } draws a random variable from the range low to high , where each number has an equal chance of being selected
size refers to the shape of the data requested
```python
xs = np.random.uniform(-10,10,(observations,1))
```
this observations size is due the recommended size of [ observations by parameters ]
so our training data is essentially just sets of 10,000 randomly generated numbers
they range from -10 to 10 and are in the shape : [ 10,000 , 1 ]
```python
zs = np.random.uniform(-10,10,(observations,1))
```


format into one unut for passing to the model:
theory states our training data should be shape n x k ; or 
observations by variables ; 10,000 x 2 ; x & z
```python
inputs = np.column_stack((xs,zs)) # stacks columns ; 10,000 rows by 2 columns
print(inputs.shape)
```

noise for data leniency
```python
noise = np.random.uniform(-1,1,(observations,1))
```

we need to generate targets
we are going to set the optimal weights to be 7 for x's and -14 for z's ; this makes a linear relationship throughout the model the optimal function for the machine. Also, our data is dual-variable, not multi, so 3 dimensional data would not be able to be input, assessed, or optimized.
```python
targets = 7 * xs + -14 * zs + 5 + noise # add noise
print(targets.shape)
```

the dude glossed over this and it is unecessary but i think its interesting
```python
#targets = targets.reshape(observations,)
#fig = plt.figure()
#ax = fig.add_subplot(111,projection='3d')
#ax.plot(xs,zs,targets)
#ax.view_init(azim=100)
#plt.show()
#plt.close() # the library is outdated
```
it was supposed to show our data on a 3d plane ; I think in preparation for some dimensional collapse we'll do soon


Generate the weights - i_range is range for weights & biases
```python
i_range = 0.1

weights = np.random.uniform(-i_range, i_range, size = (2,1))
biases = np.random.uniform(-i_range, i_range, size = 1)

print(f"Weights and Biases:\n{weights},{biases}\nAnd their shape:\nWeights Shape:{weights.shape} \nAnd Biases Shape:{biases.shape}")