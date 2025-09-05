Previously, we made a model with a single layer, and linear definition
	the model had no curves or changes through the slope
		it had multiple inputs, but it optimized each input off of linear functions

a non-linear function example is the [ Sigmoid Function ]$$\text{Sigmoid} = \sigma (x) = \frac{1}{1+\epsilon^{-x}}$$
	the inputs of something like our model computing a linear output from the input { y = xw + b } with the Sigmoid Function applied consecutively would constitute One Layer of a Neural Network
		this is the building block of Neural Nets, and they usually consist of many blocks
			all together, this is a Deep Net

Deep Nets
	layers of ' neurons ' or ' nodes ' organized by layer and interconnected within ; every ' neuron ' of layer 0 connects to every ' neuron ' of layer 1 
			Notation for a Network is as follows :
				The initial layer of the network is layer 0 { like python }
				The last layer of the network is layer L-1, the ' output ' layer { where L = len( layers ) }
							This layer is responsible for the values that we compare the the targets for loss and gradient calculations
				All layers between layer 0 and layer L-1 are Hidden Layers
							This refers to the 'black box ' nature of Deep Networks, we know they exist, their size, their orientations ; we never find out what they actually do, however. This is left the model {{ Machine Learning ! }}.
				The ' width ' of a layer is the number of ' neurons ' in said layer 
				The 'depth ' of a network is the number of layers in said network
					The ' width ' and ' depth ' of a network constitute its [ Hyperparameters ]
						Weights and Biases are the [ Parameters ] of the Model
							Hyperparameters are preset by architects of the model ; the parameters are found by the model through optimization
				Every ' neuron ' of layer x is connected to every ' neuron ' of layers ( x + 1 ) & ( x - 1 )
					every layer and node is completely ' wired in '