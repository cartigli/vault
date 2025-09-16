model = tf.keras.Sequential([ # tf = tensor flow ; keras 
							tf.keras.layers.Dense(output_size)
							]) # this completes the definition of our model
					^ This was our previous initialization of the model. We initialized our weights with random variables between two points using the NumPy's random.uniform() fx in another portion of the code , but we can consolidate our model's definitions and initializations

*Instead of the sole argument of output size being passed to the model , we can add arguments for weight and bias initialization , using the same methodology as before. 
	Also, weights are referred to as **kernels** in this context*

model = tf.keras.Sequential([
			tf.keras.layers.Dense(
				output_size,
				kernel_initializer=tf.random_uniform_initializer(minval = -0.1, maxval = 0.1),		
				bias_initializer=tf.random_uniform_initializer(minval = -0.1, maxval = 0.1)
				)
		]) 
*In the previous script, we employed the SGD, or Scholastic Gradient Descent methodology for gradient calculations, defined in ' model.compile() '. We can also introduce the learning rate as a argument of Tensor Flow's optimizer library for SDG, which optimizes descent, learning rate, decay, etc.,*
```python
#*custom_optimizer = tf.keras.optimizers.SGD(Learning Rate) for now, but there are more optional args*
custom_optimizer = tf.keras.optimizers.SGD(learning_rate=0.01) # now this is our optimizer
```

old:
model.compile(optimizer='sgd', loss='mean_squared_error')*
new:
```python
model.compile(optimizer=custom_optimizer, loss='mean_squared_error')
```

model.fit() remains unchanged
```python
model.fit(training_data['inputs'], training_data['targets'], epochs=100, verbose=2)
```