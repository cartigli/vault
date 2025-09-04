```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D


#generate training data ; linear relationship within

observations = 10000 # n

#2 variable linear model ; x & z

#{ np.random.uniform (low,high, size) } draws a random variable from the range low to high , where each number has an equal chance of being selected
#size refers to the shape of the data requested
xs = np.random.uniform(-10,10,(observations,1))
#this observations size is due the recommended size of [ observations by parameters ]
#so our training data is essentially just sets of 10,000 randomly generated numbers
#they range from -10 to 10 and are in the shape : [ 10,000 , 1 ]
zs = np.random.uniform(-10,10,(observations,1))




#format into one unut for passing to the model: training data should be shape n x k 
inputs = np.column_stack((xs,zs)) # stacks columns ; 10,000 rows by 2 columns
print(f"\nInput\'s shape:{inputs.shape}")


#noise for data leniency
noise = np.random.uniform(-1,1,(observations,1))

#we need to generate targets
#we are going to set the optimal weights to be 7 for x's and -14 for z's 
#this makes a linear relationship for the targets
targets = 7 * xs + -14 * zs + 5 + noise # add noise
print(f"\nTarget\'s shape:{targets.shape}")



#Generate the weights - i_range is range for weights & biases
i_range = 0.1 # inputs x 2 is the range of values they can initially take

weights = np.random.uniform(-i_range, i_range, size = (2,1))
biases = np.random.uniform(-i_range, i_range, size = 1)

print(f"Weights and Biases:\n{weights},{biases}\nAnd their shape:\nWeights Shape:{weights.shape} \nAnd Biases Shape:{biases.shape}")

learning_rate=0.1
```


























outputs = np.dot(inputs,weights)

# train the model
def train(inputs,weights,outputs):
	for i in range (100):
		# give the input data to the weights / mode
		weights = ouputs - learning_rate*(-7+outputs)
		#biases = ouputs - learning_rate*(-7+outputs)
		Loss = inputs - targets

train(inputs,weights,outputs)