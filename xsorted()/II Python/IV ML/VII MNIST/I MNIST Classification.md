Dataset of 70,000 handwritten numbers

We want a model to take the input of the numbers and correctly predict the number
Created by Yan LeCun, Corinna Cortes, and Christopher Burges

Every image is 28 x 28 pixels, so a 28 x 28 matrix of pixels. The images are on a gray scale from 1-255, so each pixel will have a value from 1 - 255 that denotes its grayscale intensity { white is 255, black is 0 }. So now we have a 28 x 28 matrix of values ranging from 1 to 255. We will split this data by row and connect them in a vector of length 784. 

This means the input layer of the model will be 784 neurons wide. One for every pixel of every image in the MNIST dataset. It is tasked with outputting prediction of the number, so it will have 10 neurons in the output layer.

The model is making categorical predictions based on probabilities, so we'll use One Hot encoding for the targets and outputs and softmax activation for the outputs

We need to:
- Prepare and process the data
	- Create training, validation, and testing datasets
		- As well as batch size
- Outline the model and choose the optimizers and a loss function
- Make it learn { back propagate } and validate after every epoch