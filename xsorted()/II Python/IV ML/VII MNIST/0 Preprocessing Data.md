Compatibility, orders of magnitude, Generalization

Often, we want relative values instead of value.

Log transformations are done to relative data to better show patterns among complex datasets.

Standardization : Feature Scaling
Transform the data your using is standardized with a mean of 0 and a standard deviation of 1
	Subtract every data point or feature from the mean of the data set and divide by the standard deviation
		$\frac{x-\mu}{\sigma}$


There's also PCA and Binary Encoding

Principal Components Analysis is a dimension reduction technique  ; groups variables of similar meaning into one dimension
Whitening is often done after PCA and removes underlying correlations between the data points, when these correlations are seen in the outputs.

For categorical data, we need a way to make cetegories into numbers so we can judge the model
One Hot and Binary

Binary Encoding
Say your store sells bread, muffins, and yogurt 
$$\begin{matrix}
x & | & Numerical & | & Binary \\
Bread & | & 1 & | & 0 & 1 \\
Muffin & | & 2 & | & 1 & 0 \\
Yogurt & | & 3 & | & 1 & 1 \end{matrix}$$
	Bread = 1, Muffin = 2, Yogurt = 3 has unintended implications of order and magnitude between the categories ; muffin is twice bread and bread is $\frac{1}{3}$ yogurt 
	Binary encoding : Bread - 01, Muffin = 10, Yogurt = 11
		Much more informative without bias, but still suggests that 1 of muffin is the opposite of bread, and vice versa, whatever is not bread is muffin and what is neither is yogurt

One Hot 
Binary encoding but one column per variable of the dataset 
$$\begin{matrix}
x & B & M & Y \\
Bread & 1 & 0 & 0 \\
Muffin  & 0 & 1 & 0 \\
Yogurt & 0 & 0 & 1 \end{matrix}$$
	Bread = 100, Muffin = 010, Yogurt = 001
		These has the least underlying correlation between variables
			We say a hypothetical model using this to classify horse, cat, or dog pictures
				[ 1, 0, 0 ] is a horse, [ 0, 1, 0 ] is a cat, and [ 0, 0, 1 ] is a dog
			This works well when we need uncorrelated categories, but if we have many columns, Binary Encoding becomes much more efficient 
						If we have 15,000 categories, we'd use binary as we could compress them into only 16 columns