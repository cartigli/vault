Before anything, preprocessing is initial step of all ML
	for Naive Bayes, preprocessing requires special attention to tokenization and vectorization
		Tokenization
			initially needs to be broken into manageable chunks called Tokens
				these tokens are words or phrases the algo with analyze as individual elements
		Vectorization
			we need to convert these tokens to numbers , for the algorythm to be able to accept as input
				encodes tokens as numerical values
					common strategy is making them into an array; each number denotes the presence or frequency in the text

testing text, or testing data, is tokenized and vectorized in the same way, so the model can make the same type and quality prediction as it did during training





step 2 is define x and y; input data and target
	Features
		input data ; categorized 
		independent 
	Target
		optimal prediction of the model
		correct response 

Split data 
	split into training and test data
		with training, it finds and confirms patterns, develops algo
		with testing, we can determine how generalizable the algo is and how well fit the machine's algorithm has become
			*note: the model does not have prior access and was not trained on any of the contents of the training data*

Train the Model
	run algortyhm, repeat

Evaluate Model
	Confusion Matrix is good example
	measure on things like accuracy, precision, 