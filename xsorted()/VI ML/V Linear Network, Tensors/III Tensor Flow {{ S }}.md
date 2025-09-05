```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow as tf
import os

file_path = '/tmp/TF_intro'

# generate data
observations = 1000

xs = np.random.uniform(-10,10,size=(observations,)) # training data
zs = np.random.uniform(-10,10,size=(observations,)) # training data

generated_inputs = np.column_stack([xs,zs]) # inputs for model

noise = np.random.uniform(-1,1,size=(observations,)) # noise for leniancy

generated_targets = 2 * xs - 3 * zs + 5 + noise # targets for model

# tensor flow deals with tensors and doesn't handle data sets well, atleast ones in .csv or excel formatting
# we can save the training data for tensor flow in .npz format ; numpy's go to and an easy one for tensor flow to read and use
# it saves this .npz file on your device ; it can be reopened , copied , edited , just like any database

np.savez(file_path, inputs=generated_inputs, targets=generated_targets)



# define & use our model

# not strictly necessary here
training_data = np.load(file_path+'.npz') # load the data we just saved ^

# define the model's params
input_size = 2 # two variables ; xs and zs stacked
output_size = 1 # single prediction per 2 inputs 

#tf.kera.Sequential([ ]) specifies how the model will be layed out , or howe the ' layers ' will be ' stacked '
# tf = tensor flow ; keras = the module ; Sequential takes the args we lay down as layers

# previously , we made a model where outputs = np.dot(inputs, weights) + b
# tf.keras.layers.Dense(ouyput_size) takes the inputs provided to the model and calculates the dot product of the inputs and weights plus the bias - everything we did with outputs = np.dot(inputs, weights) + biases 

# note that this function also by default intializes out weights and biases ; we never specify how we want them so they were intialized under xavier uniform for weights and zeros for bias , which is fine , but annoying it was not mentioned
model = tf.keras.Sequential([ # tf = tensor flow ; keras 
							tf.keras.layers.Dense(output_size)
							]) # this completes the definition of our model

# model.compile(optimizer,loss) configures the model for training
# SDG = Stpchastic Gradient Descent ; optimization algorithm for our model
# loss is calculated as the mean_squared_error ; objective fx
model.compile(optimizer='sgd', loss='mean_squared_error') # ='sgd' includes the learning_rate=0.01 as default 


# only thing left it to indicate to the model which data to fit
# model.fit(inputs, targets) trains the model on inputs , computing loss with respect to targets
# one epoch = one full cycle of all training data ; set in model.fit()
#model.fit(training_data['inputs'], training_data['targets'], epochs=100, verbose=0) # from .npz , no outputs for epochs / loss
#model.fit(training_data['inputs'], training_data['targets'], epochs=100, verbose=1) # list epochs & loss , respectively
model.fit(training_data['inputs'], training_data['targets'], epochs=100, verbose=2) # cleaner output than 1


# targets = 2 * xs - 3 * zs + 5 + noise = equation
# model is the model we made and defined above, the layers required an input and we only have 1 layer , so 0
# get weights is the method that returns the final values the training process output for weights 
params = model.layers[0].get_weights() # gives two arrays ; one for weights and another for bias -- weights is an array of two values , bias is an array of one value
print(f"\n\nParameters of the model after training:\n{params}")

#weights = model.layers[0].get_weights(0)
weights = model.layers[0].get_weights()[0]

#biases = model.layers[0].get_weights(1) 
biases = model.layers[0].get_weights()[1]

print(f"\nWeights:{weights}, \nBiases:{biases}")



# prediction of values by the model ; testing
# model.predict_on_batch(data[ ]) calculates outputs given inputs
#print(model.predict_on_batch(training_data['inputs']).round(1)) # the output of this fx is the data the model compares to the targets to determine loss and accuracy of every epoch
#training_data['targets'] are the values the output of predict is compared against
#print(f"\n\n{training_data['targets'].round(1)}")
# obviously, visually scanning thousands of input and output pairs is inefficient 
# we can plot the points instead

plt.plot(np.squeeze(model.predict_on_batch(training_data['inputs'])),np.squeeze(training_data['targets']))
plt.title('outputs vs targets')
plt.xlabel('outputs')
plt.ylabel('targets')
plt.show()
plt.close()

print(f"\nThe tightness of this line speaks to the accuracy of the model ; the graph is concise and very near to the ideal graph of slope 45 degrees. If the model were not accurate or trained well enough, this line would be ' fatter ' and adhere less strictly to the 45 degree optimal slope.")