Preprocessing the Dataset
	Balance the Dataset
		if 90% of customers didn't repurchase, the model could predict no one will repurchase and still obtain 90% accuracy by our metrics 
			to resolve this, we balance the data set, making the groups of non purchasers equal to the purchasers
	Divide into training, validation, and test
	Save in TensorFlow friendly format

For Reuse of this Preprocessing Code:
	ascertain if the columns being slices are still correct for your data and objective
	modify the balancing functionality to properly balance your dataset equally for whatever variables you specify

```python
import os
import numpy as np
from sklearn import preprocessing

# load the dataset
raw_csv_data = np.loadtxt('/Volumes/HomeXx/compuir/Audiobooks_data.csv', delimiter=',')

# slice out the training data ; column 1 through columns 10 [ of 0 - 12 ]
unscaled_inputs_all = raw_csv_data[:,1:-1]
targets_all = raw_csv_data[:,-1]

# shuffle dataset before balancing / standardizing
shuffled_unscaled_indices = np.arange(unscaled_inputs_all.shape[0])
np.random.shuffle(shuffled_unscaled_indices)

unequal_inputs_all = unscaled_inputs_all[shuffled_unscaled_indices]
unequal_targets_all = targets_all[shuffled_unscaled_indices]


# balance the dataset's 1's and 0's
num_one_targets = int(np.sum(unequal_targets_all))
zero_targets_counter = 0 # make a counter starting at 0
indices_to_remove = [] # empty list

for i in range(unequal_targets_all.shape[0]): # for all the values in the first column of targets { which is all of them as targets has one column }
	if unequal_targets_all[i] == 0:
		zero_targets_counter += 1
		if zero_targets_counter > num_one_targets:
			# .append() adds objects to a list
			indices_to_remove.append(i) # add extra 0 to delete list

unscaled_inputs = np.delete(unequal_inputs_all, indices_to_remove, axis=0)
unscaled_targets = np.delete(unequal_targets_all, indices_to_remove, axis=0)


# scale the inputs, standardize the data
inputs = preprocessing.scale(unscaled_inputs)
targets = unscaled_targets


# create the training / validation / testing split | 80 10 10
samples_count = inputs.shape[0] # length of inputs left
train_samples_count = int(0.8*samples_count)
val_samples_count = int(0.1*samples_count)
test_samples_count = samples_count - val_samples_count - train_samples_count

# slicing arrays
# [ start : stop : step ]
# train is from 0 to the train_sample count
# val is from the train sample count to the train sample count + val sample count
# test is from the train samples count + val sample count to the end

train_inputs = inputs[:train_samples_count]
train_targets = targets[:train_samples_count]

val_inputs = inputs[train_samples_count:train_samples_count+val_samples_count]
val_targets = targets[train_samples_count:train_samples_count+val_samples_count]

test_inputs = inputs[train_samples_count+val_samples_count:]
test_targets = targets[train_samples_count+val_samples_count:]


# save the processed data in useable & accessible format
np.savez('/tmp/ab_train_data',inputs=train_inputs, targets=train_targets)
np.savez('/tmp/ab_validation_data',inputs=val_inputs, targets=val_targets)
np.savez('/tmp/ab_test_data',inputs=test_inputs, targets=test_targets)
```