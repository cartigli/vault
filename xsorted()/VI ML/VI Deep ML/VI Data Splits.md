Training data we know

Validation is testing for overfitting ; if the loss of the training process decreases while the loss for the validation dataset increases, overfitting is occurring
	if the levels of loss are equal, continue training

Testing Dataset is for the final calculation for the model's accuracy ; however well the model does on the testing data is equal to the models accuracy
		training and validation accuracy are only subcomponents and are not factored into this calculation of the actual model's accuracy

N-Fold Cross Validation
	this is for datasets under the optimal size for training
		if we cannot afford an appropriate split between training, validation, and testing, the validation and training sets can be combined when using N-Fold Cross Validation
				say we have 11,000 data points in total. We'll give 1,000 to Testing and 10,000 to Training and Validation
						we split this into 10 chunks of 1,000 data points, denoting the 1st chunk as validation and the consequent 9 as training
								we run the first epoch as usual and then, once completed, we move the validation set to the second 1,000 point chunk, and pose the rest as training
										in this way, after every epoch, the model is validated on data it was not trained on while allowing consequent epochs on the same data set without requiring an external validation check
												obviously suboptimal compared to a genuine validation set, but still useful in cases of limited data, the likelihood of the validation red flag being triggered is just lowered, but more likely than without any warning systems in place