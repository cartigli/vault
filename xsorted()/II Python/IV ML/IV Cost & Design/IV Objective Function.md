The measure used to evaluate how well the model's prediction matches the desired values, or correct outcomes given the inputs
	{{ Loss Functions & Reward Functions }}

[ Loss Function ] : [ Cost Function ]
	The lower the cost of the function, the higher the accuracy of the model
		The model predicts 4, but the correct pair for its input was 3, the loss was 1
			The model predicts 2, but the correct pair for its input was 3, the loss was 1
				Reward is the same thing but instead of minimize cost, or loss, the model's trained to maximize the reward function
				cost : loss is much more common and widely adopted

[ Loss ] is a reinforcement function of [ Supervised Learning ]
	[ Supervised Learning ] is comprised of [ Regression ] and [ Classification ]
		Their respective cost functions are [ L2-Norm ] and [ Cross-Entropy ]

In [ Supervised Learning ] , we generally have a target : [ T ]
	This is the goal of the model ; the optimal result
	The model's output, or ' arrow ' at the target, is its predictions , denoted [ y ]
		*Generally* ; [ T ] - [ y ] = [ Loss ] for one [ epoch ] - training ' round '
			The closer to T that y is, the lower the [ Cost ] , or Loss of the model
				For a linear model, the goal would be to find a function of x that gets an output as close to the targets , the training pairs of correct outputs , but for all of the inputs and pairs. The model would take every variable x and run its computation , after which the individual losses are summed for the cost of this [ epoch ]. Then, the model adjusts the weights and biases and performs another epoch on x with the new weights and biases to generate a new total cost. The difference between epoch1 and epoch2 is the Cost Function's slope! 
						With any substantial model, there will be hundreds, if not thousands, if not millions of epochs, making the Cost Function much more complicated. Also, as we see below, it is not as straight forward with modern formulas and functions , but you get the point.

[ L2-Norm Loss Function ] : [ Regression ]
	L2-Norm = OLS
		$L2-Norm = \sum_i(y_i - t_i)^2$
			' norm ' because it is the [ Eucledian Distance ] of the outputs , y, and the targets , t , a.k.a., the [ vector norm ]`
					Lower the sum of the errors,  lower the loss`

[ Cross-Entropy ] : [ Classification ]
	Outputs are categorical , so the mathematical straightforwardness is absent
		$\text{Cross Entropy} = L(y,t) = - \sum(t_i) ln_{y_i}$
			' l of y and t is equal to minus the sum of the targets times the natural log of the outputs '

Cross-Entropy loss calculation ex:
Our model is tasked with identifying Horses, Cats, and Dogs from a series of images
-the data set is labeled with the correct classifications so we can accurately calculate accuracy and therefore , Cost
Horse = [ 1 , 0, 0 ]
Cat = [ 0 , 1, 0 ]
Dog = [ 0 , 0, 1 ]
	Model predicts [ .4, .3, .3 ] when given a picture of a Horse
				This vector equates to a prediction that the input is 40% probability of being a Horse, 30% probability of being a Cat, and 30% probability of being a Dog
		Model predicts [ .2, .1, .7 ] when given a picture of a Dog
					= this picture has a 20% probability of being a Horse, 10% probability of being a Cat, and 70% probability of being a Dog

The loss for these respective predictions is as follows:
		loss1 : [ - 0 x ln(.4) - 0 x ln(.3) - 0 x ln(.3) ]
			loss1 : [ -1 x - 0.916 - 0 x - 1.204 - 0 x - 1.204 ]
				loss1 : [ -1 x - 0.916 ]
					loss1 : [ 0.916 ]
		loss2 : [ - 0 x ln(.2) - 0 x ln(.1) - 1 x ln(.7) ]
			loss2 : [ - 0 x - 1.609 - 0 x - 2.303 - 1 x - 0.357 ]
				loss2 : [ - 1 x - 0.357 ]
					loss2 : [ 0.357 ]
Cross-Entropy Loss 2 was lower than Cross-Entropy Loss 1
	*output 2's prediction was more accurate*

Since all but the correct probability are reduced to 0 in the Cross-Entropy Loss Function , we can remove them from the formula
	$\text{Cross Entropy} = L(y,t) = - \sum(t_i) ln_{y_i}$

*Anything that is higher for worse results and lower for better results can be a loss function*