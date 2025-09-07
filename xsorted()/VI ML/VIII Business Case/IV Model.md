The dataset contains 10 columns of variables, and we are predicting a binary value
Our model will use 10 input neurons and 2 output neurons
```python
import numpy as np
import tensorflow as tf

npz = np.load('ab_train_data.npz')
trn_inputs, trn_targets = npz['inputs'].astype(np.float64), npz['targets'].astype(np.int64)
#train_inputs = npz[train_inputs].astype(np.float) # decimal
#train_targets = npz[train_targets].astype(np.int) # 1 or 0

npz = np.load('ab_val_data.npz')
val_inputs, val_targets = npz['inputs'].astype(np.float64), npz['targets'].astype(np.int64)
#validation_inputs = npz[val_inputs].astype(np.float)
#validation_targets = npz[val_targets].astype(np.int)

npz = np.load('ab_test_data.npz')
tst_inputs, tst_targets = npz['inputs'].astype(np.float64), npz['targets'].astype(np.int64)
#test_inputs = npz[test_inputs].astype(np.float)
#test_targets = npz[test_targets].astype(np.int)



input_size = 10
output_size = 2
hidden_size = 50
model = tf.keras.Sequential([
	#tf.keras.layers.Dense(input_size)
	tf.keras.layers.Dense(hidden_size, activation='relu'),
	tf.keras.layers.Dense(hidden_size, activation='relu'),
	tf.keras.layers.Dense(output_size, activation='softmax') # classifier output activation
							])

# optimizer
#MNIST
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])

BATCH_SIZE = 100

n_epoch = 100

# by default, this will stop the model the first time validation loss increases from one epoch to another
early_stop = tf.keras.callbacks.EarlyStopping()

model.fit(
	trn_inputs,
	trn_targets,
	# indicating natch size here automatically batches the data during training
	batch_size = BATCH_SIZE,
	epochs = n_epochs,
	callbacks=[early_stop], # add callback to the 
	validation_data=(val_inputs, val_targets),
	#val_inputs,
	#val_targets,
	verbose=2
	)

test_data = (tst_inputs, tst_targets)

test_loss, test_accuracy = model.evaluate(tst_inputs,tst_targets)
print(f"Test Loss:{test_loss:.2f}. Test Accuracy:{test_accuracy*100:.2f}%")