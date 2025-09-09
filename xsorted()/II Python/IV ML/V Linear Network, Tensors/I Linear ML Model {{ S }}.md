```python
import numpy as np

#generate training data ; linear relationship within

observations = 10000 # n
#observations = 100000 # n
#observations = 10000000 # n

#{ np.random.uniform (low,high, size) } draws a random variable from the range low to high , where each number has an equal chance of being selected
#size refers to the shape of the data requested
xs = np.random.uniform(-10,10,(observations,1))
#this observations size is due the recommended size of [ observations by parameters ]
#so our training data is essentially just sets of 10,000 randomly generated numbers
#they range from -10 to 10 and are in the shape : [ 10,000 , 1 ]
zs = np.random.uniform(-10,10,(observations,1))




#format into one unit for passing to the model
#training data should be shape n x k 
inputs = np.column_stack((xs,zs)) # stacks columns ; 10,000 rows by 2 columns
print(f"\nInput\'s shape:{inputs.shape}")


#noise for data leniency
noise = np.random.uniform(-1,1,(observations,1))

#we need to generate targets
#we set the targets equal to the equation of the model
#this makes a linear relationship for the targets
targets = 7 * xs + -14 * zs + 5 + noise # add noise
#targets = 7 * xs**2 + -14 * zs + 5 + noise # try non-linear fx ! - exploding gradients, false minimums, extra bs all over
print(f"\nTarget\'s shape:{targets.shape}")



#Generate the weights - i_range is range for weights & biases
i_range = 0.1 # inputs x 2 is the range of values they can initially take

# 2 weights for 2 input variables ; or shape of weights
weights = np.random.uniform(-i_range, i_range, size = (2,1))
# one bias for one output
biases = np.random.uniform(-i_range, i_range, size = 1)

print(f"Weights and Biases:\n{weights},{biases}\nAnd their shape:\nWeights Shape:{weights.shape} \nAnd Biases Shape:{biases.shape}")

#learning_rate=0.005 # restrict correction via gradient descent 
learning_rate=0.02 # too low for non linear + 10000000 observations

# calculate outputs
#         np.dot(a,b) multiplies matrices ; can also be denoted as a.dot(b)
# compare outputs to targets 
# print the loss 
# adjust weights and biases accordingly 
#      repeat 

for i in range(300):
	# input shape : 10,000x2 ; weight's shape: 2x1
	# bias is a scalar, so it is added elementwise to the results of the dot product 
	outputs = np.dot(inputs,weights) + biases
	deltas = outputs - targets # 10000x1 - 10000x1
	# regression loss is l2 norm ; sum of delta squared 
	loss = (np.sum(deltas**2)/2)/observations # l2 norm loss mean per observation - estimate | scaled over observations moves the dependency on training configuration from learning rate to more universal terms
	print(loss)


	deltas_scaled = deltas / observations # do the same for delta

	# update the weights
	# x times scaled sum of loss squared / 2 times learning rate is the value of incremental change to make to the weights
	# updated weights is equal to the weights - the sum of all losses squared and scaled dot-product'd by the inputs and adjusted by the learning rate 
	# inputs shape : 10000x2 , deltas shape : 10000x1
	# inputs.T shape : 2x10000 , deltas shape 10000x1
	# this is the computation of the gradient of the loss function with respect to weights ; np.dot(inputs.T,deltas_scaled) is the gradient calculation -- how much each weight contributed to overall error
	# this times the learning rate is the adjustment for this epoch for the weights ONLY
	weights = weights - learning_rate * np.dot(inputs.T,deltas_scaled)
	# then we calculate the loss gradient with respect to biases , adjust over the same learning rate, and subtract from the original bias to get the new
	biases = biases - learning_rate * np.sum(deltas_scaled)
	if i % 25 == 0:
		print(weights, biases) # print weights & biases every 5 epochs

#training logic is complete! this model finds the minimum cost function with brute force trial and error adn adjustments of weights and biases through gradient descent
```