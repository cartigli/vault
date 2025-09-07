usefulness: price optimization, inventory management
- goal: increase profit, minimize costs

Now that collection/preprocessing/Data analysis
transition from analysis to analytics - trend prediction

[Traditional]
- Regression [popular]
	- representing causal relationships between observations[/measurements]
	- [shown below] scatter plot of values in respect to [x, y]
	  |                                      x                 x
	  |                         x         x       x
	  |                 x                x
        	  |             x
y_axis |________________________ x_axis
		- y = house size 
		- x = size of house
		- Equation [y = m[slope]x + b[y_intercept]]
- regression aims to define a relationship between sets [pairs in this ex] of data
- tries to find trend instead of perfect fit; much more interpretable measurement
	- in this ex, size of house increases = price increases
[Clustering] - group observations
- find collections and groups standing out from whole
- more closely related between themselves than the group as a whole
- [below] scatter plot of values in respect to [x, y]
	  |            x         x
	  |                 x        x         x     x  x
	  |                 x                x  x      x
        	  |                                              x
y_axis |________________________ x_axis
- x = price of house
- y = size of house
	- now, we see two clusters of 'outliers' 
		- small house but higher price
		- large house but lower cost
[Factor Analysis] - grouping explanatory variables
- Ex: 100 question survey
- 1. I like animals [1-5]
- 1. I care about animals [1-5]
- 1. I am against animal cruelty [1-5]
	- one can assume if someone responds 5 for 1, they'll likely continue with high score responses for q2 & q3
	- from this, we could assume relevancy/relationship between the q's and responses
	- use this relationship to combine all q's into 'general attitude towards animals'
		- repeated over 100 question survey:
		- variables decrease from 100 to a multiple of 100 [factorally scale database size]

[Time Series] - plotted values on T.time
- time is *always* on the x_axis
