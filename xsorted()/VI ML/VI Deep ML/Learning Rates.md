Hyperparameters are set by us, like the width, depth, and $\eta$ of the network

$\eta$, or the Learning Rate, is rate at which the model is allowed to modify its weights in respect to the cost gradient

Learning rate Schedule
	to optimize, we start with high training rates to facilitate big patterns and initial discoveries
		we lower it as the model progresses through the data so it does not overfit as patterns it adopts become more specific
				ex:
					First 5 epochs : $\eta = 0.1$
					Second 20 epochs : $\eta = 0.01$
					Third 100 epochs : $\eta = 0.001$
				A more modern solution is an exponential learning rate based on the number of epochs. 
					for n in range(epochs):
						$\eta = \eta_0  e^{-n / c }$
					so in the exponent of e, n is the current epoch and c is some constant
						c can be a range of values but its around the number of epochs needed to minimize the cost
							if this is around 100 epochs, c could be from 50 - 500
							if this is around 1000 epochs, c could be from 500 - 5000
								c is another Hyperparameter of the model