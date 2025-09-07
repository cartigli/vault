```python
import os
import numpy as np
from sklearn import preprocessing

# load the dataset
raw_csv_data = np.loadtxt('/Volumes/HomeXx/compuir/Audiobooks_data.csv', delimiter=',')

# slice out the training data ; column 1 through columns 10 [ of 0 - 12 ]
unscaled_inputs_all = raw_csv_data[:,1:-1]
targets_all = raw_csv_data[:,-1]

num_one_targets = int(np.sum(targets_all))
zero_targets_counter = 0 # starts at 0
indices_to_remove = [] # empty list

for i in range(targets_all.shape[0]):
	if targets_all[i] == 0:
		zero_targets_counter += 1
		if zero_targets_counter > num_one_targets:
			indices_to_remove.append(i) # add extra 0 to delete list

unscaled_inputs_equal_priors = np.delete(unscaled_inputs_all, indices_to_remove, axis=0) # balance inputs and targets of 1's and 0's
targets_equal_priors = np.delete(targets_all, indices_to_remove, axis=0)

# scale the inputs, standardize the data
scaled_inputs = preprocessing.scale(unscaled_inputs_equal_priors)

shuffled_indices = np.arange(scaled_inputs.shape[0]) # generate customer indices
np.random.shuffle(shuffled_indices) # shuffle indices

shuffled_inputs = scaled_inputs[shuffled_indices] # set as inputs
shuffled_targets = targets_equal_priors[shuffled_indices] # set as training

# create the training / validation / testing split | 80 10 10
samples_count = shuffled_inputs.shape[0] # length of inputs left

train_samples_count = int(0.8*samples_count)
validation_samples_count = int(0.1*samples_count)
test_samples_count = samples_count - validation_samples_count - train_samples_count

train_inputs = shuffled_inputs[:train_samples_count]
train_targets = shuffled_targets[:train_samples_count]

validation_inputs = shuffled_inputs[:train_samples_count:train_samples_count+validation_samples_count]
validation_targets = shuffled_targets[:train_samples_count:train_samples_count+validation_samples_count]

test_inputs = shuffled_inputs[train_samples_count+validation_samples_count:]
test_targets = shuffled_targets[train_samples_count+validation_samples_count:]

# save the processed data in useable format
np.savez('/tmp/ab_train_data',inputs=train_inputs, targets=train_targets)
np.savez('/tmp/ab_validation_data',inputs=validation_inputs, targets=validation_targets)
np.savez('/tmp/ab_test_data',inputs=test_inputs, targets=test_targets)

