Matrix of Matrices ; many scalars is a vector, many vectors are a matrix, many matrices are a [Tensor]
	scalar : tensor rank 0
	vector : tensor rank 1
	matrix : tensor rank 2

Sklearn and Tensor are head to head 
	google developed Tensor flow for internal ML purposed
		released to the public in 1015 ; utilizes the CPU's and GPU's of host machine
			Google also released TPU's which accelerate their performance
		Tensor Flow is key for Neural Networks and complex matrices operations
			Sklearn is better for mathematical computations, preprocessing

History of Tensor Flow
Tensor Flow 1 - standard, but confusing and complex
	this led to PyTorch and Keras ; 
		Keras was later adopted into Tensor Flow { both open-sourced }
			Keras us sometimes referred to as an interface for Tensor Flow

We first see Tensor Flow 2 around 2019
	it adopted Keras and they became synonymous 
		versatility of Keras and power of Tensor
			boasts ' Eager Execution ' or standard python practices / physics apply

Our previous ML Model required $\sim$ 20 lines of code, and with Tensor Flow , it will be similar
	for later networks that would take $\sim$ 150 lines of code with alone NumPy, Tensor makes it $\sim$ 20