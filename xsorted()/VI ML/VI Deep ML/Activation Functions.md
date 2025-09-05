Non-linear, usually normalizing functions for weights and biases

Sigmoid Function : $\sigma (x) = \frac{1}{1+\epsilon^{-x}}$
	*derivative* : $\sigma(x)(1-\sigma(x))$
			this ranges form 0-1, and sort of behaves like a biological neuron
				low values are exponentially low and high numbers are exponentially high
					similar to people neurons, this acts as a sort of energy for the neuron; its firing
							when then model's neurons are given certain values, they can ' fire ' indicating information or signaling that can be interpreted as such

TanH : Hyperbolic Tangent : $\text{tanh}(a) = \frac{\epsilon^a-\epsilon^{-a}}{\epsilon^a+\epsilon^{-a}}$
	*derivative* : $\frac{4}{(\epsilon^a+\epsilon^{-a})^2}$
	 ranges from -1 to 1, similar to the sigmoid function but more normally distributed over 0

Softmax Function: $\sigma_i(a) = \frac{\epsilon^{a_i}}{\sum_i\epsilon^{a_i}}$
	*derivative* : $\frac{\partial \sigma_i(a)}{\partial a_i} = \sigma_i (a) (\delta_{ij} - \sigma_i(a))$ where $\delta_{ij}$ is 1 if i=j, 0 otherwise
			this is the normalization we would use for the outputs of the classification model as it outputs a probability ; all the results sum to 1