Supervised, Unsupervised, Reinforcement

[Supervised]
	like the weather example ; the model runs through data ; the output is judged by ' correctness ', and the optimization fx revises the weights and biases before re-running the data to find the resulting optimization fx

[Unsupervised]
	no goals, or parameters ; the goal is to have the model learn and classify the data by more efficient methods than could be manually programmed
		doesn't need labeled data or objective targets
			useful when the goal is to split data into x categories , when we don't know how to split the data , by what metrics, or how many clusters , k , to make {{ k-means clustering ! }}
[Reinforcement]
	like training your pet ; give it a treat every time a goal is achieved or metric improved

[Supervised] is the Good Stuff
	two main branches ; Classification and Regression
		Classification : cats , dogs , lizards
			Categorical : sorting, groups, clusters
		Regression : 1.32 , 1.30 , 1.27
			Numerical - predicting continuous trends or patterns 