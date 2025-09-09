the original , most fundamental Optimization Algorithm

[ Gradient Descent ] is the multivariate generalization of the derivative of the [ Cost Function ]

quick derivatives :
	$f(x) = 3x^2 + 5x + 1$
	$f'(x) = 2*3x + 5 + 0$
		$f'(x) = 6x + 5$
			*the derivative is denoted with : '
				*the derivative of f(x) is f'(x)*

suppose we want to find the minimum of the function : $x$ {{ above }}
	if we used the gradient slope method
		we take the derivative 
			$f'(x) = 6x + 5$
		we generate a random number to start
			x = 7
		and determine accuracy
-
		then, we update the model, given the new loss
			$x_0 = 7$
			$x_1 = ?$
			$x_{i+1} = x_i - \eta f'(x_i)$
			$x_{1} = x_0 - \eta f'(x_0)$
			$x_{1} = 7 - \eta f'(7)$
			$x_{1} = 7 - \eta(47)$
$$\eta=\text{Learning Rate}$$
						*let's make eta, or $\eta = 0.01$
				$x_{1} = 7 - (0.01 * 47)$
				$x_{1} = 7 - 0.47$
				$x_{1} = 6.53$
		we choose the learning rate for each case*
				*the model would then run the x of 6.53 back through the function, generate a new loss and find the new updates for the weights / biases 
					this process repeats until the rate of learning plateaus or minimizes
				eventually, the values will stop decreasing , which is the minimum cost
						the derivative = the slope of a function , so when the derivative of our loss function is no longer getting lower , we know the cost is at a minimum. Ideally and theoretically, we want a cost of 0 which means the function is completely optimized. This is a fallacy, unfortunately. We only go until we can go no further.
									Something daunting that is not important at this stage is local minimum ; when the derivative is looking for minimum too aggressively, it can get stuck in a place where the cost function dips, a local minimum, rather than the global minimum. The model will stop learning as the optimization function and derivative adjustments of weights and biases are designed to direct the model **down** the cost gradient. Another non-trivial component to fix with convoluted calculus, but we will persist.
-
	This adjustment of the weights & biases in respect to their partial derivatives is the backend behind the visualization of a hiker on a mountain or a ball on a plane ; the derivative finds the slope and points us to to a lower cost ; we know at any given moment which direction is down but we only ever know know this for the exact position we're currently in ; we are blind and the Cost Gradient is our only walking pole. At any given moment , when we calculate the partial derivatives of the weights and biases , we determine the optimal position , or value that would achieve the lowest cost function , **for the given input**. The moment we change this input variable , the cost function is completely different and could have polarizing values to the last change we made. 
	This is akin to us having ' blind ' { haha } faith in the Cost Gradient - walking pole guiding us down the mountain. If we took a step and the pole told us the ' steepest ' portion of the mountain , or fastest route , was something like left at 10 o'clock and we just freaking leapt for it , odds are this is suboptimal for your health and efficiency getting down the mountain. In the same way , if we had full faith in the Cost Gradient and adjusted weights and biases willy - nilly with accordance to the Cost Gradient, we would have problems like overfitting. 
	Our model could change the weights so **anytime** a is input, b is output. This is what we want to see from inputting a, but when we give the model c, it outputs b, as well as for the inputs d and e . . . when the weight and bias adjustment is unchecked, patterns and behavior are forgotten, it is variable per variable basis.
	Overfitting happens when the models learns too aggressively, or narrowly. We implement a learning rate to minimize the impact of one adjustment of weights to allow accumulation of broader patterns and generalizations to form. Test data is particular helpful for detecting this because it is withheld from the model during training ; it could not have over specified the information within from training. 





		    v a n i s h i n g     g r a d i e n t s