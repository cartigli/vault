Latin root: SciPy Toolkit ; meaning in addition to or on top of the SciPy package
			built on NumPy, SciPy, and Matplotlib - very fast & efficient

so far, we've mostly worked with Panda's DataFrames 
			to work with our stats modeling

if we pre-process data with panda, it may need to be transformed into a ndarray for computation
			ndarray = NumPy array
			* sklearn only works with arrays, not DataFrames, so all input and processed data will have to be transformed into ndarrays *

advantages:
			thorough and extensive documentation on all innerworkings and computational methods available; they do not hide anything and are thoroughly monitored & kept up-to-date
			-
			in terms of machine learning, Sklearn holds the lead with variety of available options, like regression, classification, clustering, SVM's, dimensionality reduction
						for deep learning has tensorFlow, pyTorch, Keras lead over Sklearn
			-
			Numerical Stability with Sklearn is superb; infinitely small numbers like vanishing gradients can be further corrupted by programs with faulty monitoring and tracking of such inherently unstable values

we'll do the same examples as with Panda but with sklearn
			scripts denoted with ' {{ S }} '