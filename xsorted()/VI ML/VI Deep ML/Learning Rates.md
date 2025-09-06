Hyperparameters are set by us, like the width, depth, and $\eta$ of the network

$\eta$, or the Learning Rate, is rate at which the model is allowed to modify its weights in respect to the cost gradient

Learning rate Schedule
	to optimize, we start with high training rates to fascilitate big patterns and initial discoveries
		we lower it as the model progresses through the data so it does not overfit as patterns it adopts become more specific
				ex:
					First 5 epochs : $\eta = 0.1$
					Second 20 epochs : $\eta = 0.01$
					Third 100 epochs : $\eta = 0.001$