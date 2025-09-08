[ Neural Networks ] work by taking inputs and giving outputs

they are a series of inter-layered neurons configured with weights and biases

ex: we want model to predict weather based on the previous 5 days
	we give it 5 days of weather, have it predict, and adjust the weights and biases depending on how correct or incorrect the model was
		{{ gradient descent }}

the model is never explicitly told what it is intended to do, and it is never told how to do it, but through training, rewards, and punishments, the model can develop an 'intuition' and reliable method for solving the problem intrinsically
		input = previous 5 days' weather ; output = prediction for next day

could be trained on / built to predict: voice patters, phrasing or connotations, image classification, stocks, war, prices

Req:
	data - text, images, weather
	model - linear { simplest }, non-linear, neural networks, 
	objective function - estimation of ' how correct ' the model is
	optimization algorithm - adjusts weights & biases

Process:
	Give data to the model ; process it
		analyze ' correctness ' of output
			optimize weights & biases 
				repeat