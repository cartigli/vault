```python
import os
import numpy as np
import tensorflow as tf
import tensorflow_datasets as tfds

# HYPERPARAMETERS
# buffer_size - number of samples shuffled at one time
# batch size - samples in each batch
# input / output layers [ not easily changeable ]
# hidden layer sizes
# epoch count
# optimizer functions
# loss function 
# validation / training percentage split
# learning rate must be defaulting

data_dir = '/Volumes/HomeXx/compuir/tf_data'

mnist_dataset, mnist_info = tfds.load(name='mnist', with_info=True, as_supervised=True)
#mnist_dataset, mnist_info = tfds.load(name='mnist', data_dir=data_dir, with_info=True, as_supervised=True)
# as_supervised=True loads the dataset as two tuples [input, target]
# mnist_info has things like sample count, version no, etc.

mnist_train, mnist_test = mnist_dataset['train'],mnist_dataset['test']
# by default, mnist has test and training but no validation

# lets take 10% of training for validation
# set it equal to 0.1 of the number of training examples from mnist_info
num_validation_samples = 0.1*mnist_info.splits['train'].num_examples

# ensure this number is an integer, not some float
# tc.cast(x,dtype) converts a variable into a given data type
num_validation_samples = tf.cast(num_validation_samples, tf.int64)

# do the same for testing data and cast to an integer
num_test_samples = mnist_info.splits['test'].num_examples
num_test_samples = tf.cast(num_test_samples, tf.int64)


# scale the inputs so we have values between 0 and 1
# this caused warnings in the obsidian notebook env so convert to .py or add this line
@tf.autograph.experimental.do_not_convert
def scale(image, label):
	image = tf.cast(image, tf.float32) # ensure images are ints
	# all values on the grayscale are 0 - 255, so we'll divide by 255
	#image = image / 255
	image/= 255. # . means float value
	return image, label

# there is also dataset.map(function) which applies a custom transformation to a given dataset, of which is determined by the argument passed to the function
# it only works for functions that input and return an item and a label
scaled_train_and_validation_data = mnist_train.map(scale) # train / val
scaled_test_data = mnist_test.map(scale) # test 

# shuffle our data | changes order but not information within
# we want randomly spread, not ordered or organized
BUFFER_SIZE = 10000 # because we cannot load the whole 70,000 images into memory for shuffling, we shuffle 10,000 at a time
# if buffer_size = 1, nothing would happen

shuffled_train_and_validation_data = scaled_train_and_validation_data.shuffle(BUFFER_SIZE)

# pull validation set from training set 
validation_data = shuffled_train_and_validation_data.take(num_validation_samples)

# all but validation data
train_data = shuffled_train_and_validation_data.skip(num_validation_samples)

# set the batch size
# batch_size = 1 = Stochastic Gradient Descent
# batch_size = # of samples = Single Batch Gradient Descent
BATCH_SIZE = 100

# overwrite the variable as this will only ever be used as training
# adds another column to the tuple indicating the sample count per batch
train_data = train_data.batch(BATCH_SIZE)

# validation data is only fed forward, not backward, so it needs only one batch as it will not be updating weights ; we only need the accuracy
validation_data = validation_data.batch(num_validation_samples) # the whole set is one batch
# same thing for testing data
test_data = scaled_test_data.batch(num_test_samples)


# iter is the pytohn syntax for making the data set iterable 
# pairs validation input data to the corresponding label for the target in the tuple
validation_inputs, validation_targets = next(iter(validation_data))



# outline the model
# as discussed, input layer will be 784 inputs and output will be 10
# we will set the width and depth of the model
input_size = 784
output_size = 10
hidden_layer_size = 50 # assumes all hiddden layers are equal in size

# define the model with tf.kera.Sequential() stacking layers
model = tf.keras.Sequential([
						# flatten the input data into something the model can take
						tf.keras.layers.Flatten(input_shape=(28,28,1)), # not (784,0)?
						# the first hidden layer's size + choose act. function
						tf.keras.layers.Dense(hidden_layer_size, activation='relu'),
						# second layer in the same way
						tf.keras.layers.Dense(hidden_layer_size, activation='relu'),
						# define output layer
						tf.keras.layers.Dense(output_size, activation='softmax')
						])

# optimizer and loss function ; .compile() 
# tensorflow has 3 cross entropy loss functions ; binary, categorical, and sparse categorical
# only difference between cat. and sparse cat. is cat expects one-hot encoding to be already applied to the data
# we did not do this, so we apply it here
# Adam optimizer { not case sensitive }
# specify metrics you'd like returned , a.k.a., ' accuracy '
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])


# train 
n_epochs = 5

# specify training data, specify the epoch count, show validation data and the targets for validation data, return the loss, rerun the data, repeat for n = epochs
model.fit(train_data, epochs=n_epochs, validation_data=(validation_inputs, validation_targets), verbose=2)
# an example of the return:
# 540/540 - 6s - 10ms/step - accuracy: 0.8616 - loss: 0.4846 - val_accuracy: 0.9107 - val_loss: 0.3028 Epoch 2/5
#  first, we see the number of batches ; 540
# then, seconds per Epoch { 0.3028 seconds here }
# next, training loss - not valuable indiivdually but compared to those before and after
# next is accuracy ; how well outputs match the targets
# validation loss and accuracy ; 
# validation loss is to watch for overfitting
# validation accuracy is the true accuracy for the epoch ; the last value of the last epoch is the accuracy of your model



# test the model
test_loss, test_accuracy = model.evaluate(test_data)
print(f"Test Loss:{0:.2f}. Test Accuracy:{1:.2f}%.format(test_loss,test_accuracy*100.))