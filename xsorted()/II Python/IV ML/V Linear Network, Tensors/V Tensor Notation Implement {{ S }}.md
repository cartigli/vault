model = tf.keras.Sequential([
			tf.keras.layers.Dense(
				output_size,
				kernel_initializer=tf.random_uniform_initializer(minval = -0.1, maxval = 0.1),		
				bias_initializer=tf.random_uniform_initializer(minval = -0.1, maxval = 0.1)
				)
		]) 

modified model definition to use tensor Flow's weight and bias initialization in place of manual initialization
introduced custom optimizers for SDG calculations

```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow as tf
import os

file_path = '/tmp/TF_intro'

# generate data
observations = 1000 # see how it handles weird #'s

xs = np.random.uniform(-10,10,size=(observations,)) # training data
zs = np.random.uniform(-10,10,size=(observations,)) # training data

generated_inputs = np.column_stack([xs,zs]) # inputs for model

noise = np.random.uniform(-1,1,size=(observations,)) # noise for leniancy

generated_targets = 2 * xs - 3 * zs + 5 + noise # targets for model

np.savez(file_path, inputs=generated_inputs, targets=generated_targets)


# load traininf data
training_data = np.load(file_path+'.npz') # load the data we just saved ^

# define model
input_size = 2 # two variables ; xs and zs stacked
output_size = 1 # single prediction per 2 inputs 

model = tf.keras.Sequential([
	tf.keras.layers.Dense(output_size,
		kernel_initializer = tf.random_uniform_initializer(minval = -0.1, maxval = 0.1),
		bias_initializer = tf.random_uniform_initializer(minval = -0.1, maxval = 0.1)
							)
						]) # this completes the def of our model


custom_optimizer = tf.optimizers.SGD(learning_rate=0.01)

model.compile(optimizer=custom_optimizer, loss='mean_squared_error')



# model.fit(inputs, targets) trains the model on inputs , computes loss
model.fit(training_data['inputs'], training_data['targets'], epochs=100, verbose=2) # cleaner output than 1

# find results

#weights = model.layers[0].get_weights(0)
weights = model.layers[0].get_weights()[0]

#biases = model.layers[0].get_weights(1) 
biases = model.layers[0].get_weights()[1]

print(f"\nWeights:{weights}, \nBiases:{biases}")


# plot model's ' outputs ' against ' targets '
plt.plot(np.squeeze(model.predict_on_batch(training_data['inputs'])),np.squeeze(training_data['targets']))
plt.title('outputs vs targets ; model 1')
plt.xlabel('outputs')
plt.ylabel('targets')
plt.show()
plt.close()

print(f"\nThe tightness of this line speaks to the accuracy of the model ; the graph is concise and very near to the ideal graph of slope 45 degrees. If the model were not accurate or trained well enough, this line would be ' fatter ' and adhere less strictly to the 45 degree optimal slope.")