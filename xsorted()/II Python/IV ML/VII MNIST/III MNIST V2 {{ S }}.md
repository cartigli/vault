```python
import os
import numpy as np
import tensorflow as tf
import tensorflow_datasets as tfds

dest_dir = '/Volumes/HomeXx/compuir/tf_data'

mnist_dataset, mnist_info = tfds.load(name='mnist', data_dir=dest_dir, with_info=True, as_supervised=True)

mnist_train, mnist_test = mnist_dataset['train'],mnist_dataset['test']

# lets take 10% of training for validation
num_validation_samples = 0.1*mnist_info.splits['train'].num_examples

# ensure this number is an integer, not some float
num_validation_samples = tf.cast(num_validation_samples,tf.int64)

# do the same for testing data and cast to an integer
num_testing_samples = mnist_dataset['testing'].num_samples
num_test_samples = tf.cast(num_test_samples, tf.int64)


# scale the inputs so we have values between 0 and 1
def scale(image, label):
	image = tf.cast(image, tf.float32) # ensure images are ints
	# all values on the grayscale are 0 - 255, so we'll divide by 255
	#image = image / 255
	image/= 255. # . means float value
	return image, label

scaled_train_and_validation_data = mnist_train.map(scale) # train / val
scaled_test_data = mnist_test = mnist_train.map(scale) # test 

# shuffle our data | changes order but not information within
# we want randomly spread, not ordered or organized
BUFFER_SIZE = 10000 # because we cannot load the whole 70,000 images into memory for shuffling, we shuffle 10,000 at a time
# if buffer_size = 1, nothing would happen

shuffled_train_and_validation_data = scaled_train_and_validation_data.shuffle(BUFFER_SIZE)

# pull validation set from training set 
validation_data = shuffled_train_and_validation_data.take(num_validation_samples)

# all but validation data
train_data = shuffle_train_and_validation_data.skip(num_validation_samples)


# set the batch size 
BATCH_SIZE = 100

# overwrite the variable as this will only ever be used as training
# adds another column to the tuple indicating the sample count per batch
train_data = train_data.batch(BATCH_SIZE)

# validation data is only fed forward, not backward, so it needs only one batch as it will not be updating weights ; we only need the accuracy
validation_data = validation_data.batch(num_validation_samples) # the whole set is one batch
# same thing for testing data
testing_data = testing_data.batch(num_testing_samples)


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
model = tf.kera.Sequential([
						# flatten the input data into something the model can take
						tf.keras.layers.Flatten(input_shape=(28,28,1)), # not (784,0)?
						# the first hidden layer's size + choose act. function
						tf.keras.layers.Dense(hidden_layer_size, activation='relu'),
						# second layer in the same way
						tf.keras.layers.Dense(hidden_layer_size, activation='relu'),
						# define output layer
						tf.keras.layers.Dense(output_size, activation='softmax')
						])


model.compile(optmizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])


# train 
n_epochs = 5

# specify training data, specify the epoch count, show validation data and the targets for validation data, return the loss, rerun the data, repeat for n = epochs
model.fit(train_data, epochs=n_epochs, validation_data=(validation_inputs, validation_targets), verbose=2)
```
