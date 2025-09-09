Preprocessing the Dataset
	Balance the Dataset
		if 90% of customers didn't repurchase, the model could predict no one will repurchase and still obtain 90% accuracy by our metrics 
			to resolve this, we balance the data set, making the groups of non purchasers equal to the purchasers
	Divide into training, validation, and test
	Save in TensorFlow friendly format

For Reuse of this Preprocessing Code:
	ascertain if the columns being slices are still correct for your data and objective
	modify the balancing functionality to properly configure your dataset equally for whatever variables you specify

```python
import os
import numpy as np
from sklearn import preprocessing

# load the dataset
# this data is columns of information for every row of customer x 
# the first column is customer id, so we discard, and last is targets, which we don't train on
raw_csv_data = np.loadtxt('/Volumes/HomeXx/compuir/Audiobooks_data.csv', delimiter=',')

# slice out the training data ; column 1 through columns 10 [ of 0 - 12 ]
unscaled_inputs_all = raw_csv_data[:,1:-1]
targets_all = raw_csv_data[:,-1]

# balance the dataset
# count 1's, as they are less than 0's, and keep that many 0's
num_one_targets = int(np.sum(targets_all))
# make a counter for the zeros
zero_targets_counter = 0 # starts at 0
indices_to_remove = [] # empty list

for i in range(targets_all.shape[0]): # for all the values in the first column of targets { which is all of them as targets has one column }
	if targets_all[i] == 0:
		zero_targets_counter += 1
		if zero_targets_counter > num_one_targets:
			# .append() adds objects to a list
			indices_to_remove.append(i) # add extra 0 to delete list

unscaled_inputs_equal_priors = np.delete(unscaled_inputs_all, indices_to_remove, axis=0) # balance inputs and targets of 1's and 0's
targets_equal_priors = np.delete(targets_all, indices_to_remove, axis=0)

# scale the inputs, standardize the data
scaled_inputs = preprocessing.scale(unscaled_inputs_equal_priors)

# we are batch processing, so we must shuffle the data
shuffled_indices = np.arange(scaled_inputs.shape[0]) # generate customer indices
np.random.shuffle(shuffled_indices) # shuffle indices

shuffled_inputs = scaled_inputs[shuffled_indices] # set as inputs
shuffled_targets = targets_equal_priors[shuffled_indices] # set as training

# create the training / validation / testing split | 80 10 10
samples_count = shuffled_inputs.shape[0] # length of inputs left

train_samples_count = int(0.8*samples_count)
validation_samples_count = int(0.1*samples_count)
test_samples_count = samples_count - validation_samples_count - train_samples_count

# slicing arrays
# [ start : stop : step ]
# train is from 0 to the train_sample count
# val is from the train sample count to the train sample count + val sample count
# test is from the train samples count + val sample count to the end

train_inputs = shuffled_inputs[:train_samples_count]
train_targets = shuffled_targets[:train_samples_count]

# set it equal to the values between training and testing
validation_inputs = shuffled_inputs[train_samples_count:train_samples_count+validation_samples_count]
validation_targets = shuffled_targets[train_samples_count:train_samples_count+validation_samples_count]

# test is everything left
test_inputs = shuffled_inputs[train_samples_count+validation_samples_count:]
test_targets = shuffled_targets[train_samples_count+validation_samples_count:]


# save the processed data in useable format
np.savez('/tmp/ab_train_data',inputs=train_inputs, targets=train_targets)
np.savez('/tmp/ab_validation_data',inputs=validation_inputs, targets=validation_targets)
np.savez('/tmp/ab_test_data',inputs=test_inputs, targets=test_targets)
```