In our initial model, we generated weights by randomly generating values from -1 to 1
	This worked fine for us, but has a lot of important considerations for proper configuration

Initialization is the process in which we set the initial values of the weights { and biases }
	We randomly initialize weights because the entire concept behind ML is that the model has the ability to update and change these weights as it learns which ones should be set where to minimize cost 
	If the weights were all a constant, the back propagation would not distinguish between any weights , nor would forward feeding through the network. It would cripple the architecture of the network, which is why we initialize randomly. We did this in our simple ML model, but can be done with more consideration.
-
	We could also pick the weights from a normal distribution, $X \sim N(\sigma, 0)$, which is normally distributed over the mean, 0 with a standard deviation of 0.1. This, and randomly distributed initialization with equal probabilities between them, were the norm until around 2017. Both are equally problematic for our model.
	Modern Neural Network architecture uses activation functions, like the Sigmoid Function, to 'activate' the values of a neuron. High values are compressed near one, low values are compressed near 0, and values in between are usually persuaded towards one pole or the other. To deal with functions that distort higher and lower values, we need a reliable method to generate values within this range that don't immediately push the Sigmoid Function to either of its limits { vanishing gradients }.
	We do this with Xavier / Glorot Initialization, which consists of Uniform and Normal Xavier Initialization. Instead of basing the initialization of some arbitrarily chosen random value, the Xavier Initialization is based of the number of inputs and outputs, proportionally changing the size of the weights for the situation at hand. This diminishes reduction of information through the Feed Forward process and reduces the effects or symptoms of vanishing gradients.
	Xavier Uniform Initialization: 
			draw each weight, w, from a random uniform distribution in: $$[-x,x] \text{ for } x = \sqrt{\frac{6}{inputs+outputs}}$$
	Xavier Normal Initialization: 
			draw each weight, w, from a normal distribution with a mean of 0, and a standard deviation of $$\sigma = \sqrt{\frac{2}{inputs+outputs}}$$
	Xavier Initialization depends on inputs and outputs, so the more inputs and outputs a model has for w weight, the more spread out the distribution of the Xavier Initialized weight is. Note that this also happens when back propagating. This technique is the default method of TensorFlow.