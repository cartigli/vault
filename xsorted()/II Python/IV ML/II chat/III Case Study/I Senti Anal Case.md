Train a Naive Bayes Classifier with ChatGPT for Sentiment Analysis
	classifying course reviews
	process we will undergo:
		Preprocess data
		EDA
		RegEx
		ML with Naive Bias
			split training and test
			fine tune
		Model evaluation with validation set

[Naïve Bayes] Algorithm
	works well for text based work
		spam detection is very pop. application
		based on Bayes' Theorem:
			$P_{(A|B)} = \frac{P_{(B|A)} * P_{(B)}}{P_{(B)}}$
			imagine we know 30% of emails will be spam
			P( spam ) = .3, or 30%
				we also know 50% of spam contains the word 'win'
					P( Win | spam ) = 50%
					' given spam, the probability of an email containing the word ' win ' is 50% '
					' probability of win, given spam '
						$P_{( A | B )} = \frac{P_{( B | A )} * P_{( A )}}{P_{( B )}}$
						$P_{( spam | win )} = \frac{P_{( win | spam )} * P_{( spam )}}{P_{( win )}}$
								*why not $P_{(spam | win )} =$ ?? or switching the numerator's probability, like in the original formula?*
									edit: ^ I was right, video was wrong
		In Bayes' Theorem, Naïve refers to the algorithms assumption that a word in an email, like prize, as independent observations.
			For classification of ' spam ' or ' ham ' ;
				the algo looks at every word in the email db, and checks for the probability of that word occurring in mail we know is ' spam ' against those we know are ' ham '
						ex: the algo observes the word ' prize ' 100 times, 95 of which were in spam, and 5 of which were in ham
						the algo denotes ' prize ' as a 95% from spam
								then it calculates the probabilities of every word against spam...
									$P_{( spam | win )} * P_{( spam | prize )} x ...$
									combines these probabilities to determine probability of the email being spam
										if it crosses a threshold, it is classified as spam
											if not, it is classified as ham
Practical Apps:
	{{ sci-kit contains a function for running these algorithms }}
		they host Naive Bayes ; we'll use multinomial and Bernoulli for most , but 
				they also host variants like Gaussian Naive Bayes, Complement, Categorical, and Out of Core
						Gaussian, for example, presumes a distribution for word occurrence probabilities 