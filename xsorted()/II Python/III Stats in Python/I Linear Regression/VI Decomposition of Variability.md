regression equation: $\hat{y} = \beta_0 + \beta_1 x_1$

determinates of a quality/accurate model:
{{ based on the anova frameworks }}
3 qualifying and determinate factors:
	sum of squares total {{ SST }}
	sum of squares regression {{ SSR }}
	sum of squares error {{ SSE }}

[ SST ]
	sum of the difference of observed dependent variable and its mean; $\sum^n_{i=1}(y_i - \bar{y})^2$
	similar to variance, or how much variance is within the model's variables
[ SSR ] {{ ESS; explained sum of squares }}
	sum of the difference between the predicted dependent variables {{ $\hat{y}$ }} and the observed values; $\sum^n_{i=1}(\hat{y} - \bar{y})^2$
	graphically, the distance from each point and the regression model overlain; is SSR = SST; your model's prediction was perfect
[ SSE ] {{ RSS; residual sum of squares }}
	measures the unexplained variability by the regression { what SST or SSR didn't explain }
	$\sum^n_{i=1}\epsilon^2_i$

ENSEMBLE:
	{{ SST }} = {{ SSR }} + {{ SSE }}
	$\sum^n_{i=1}(y_i - \bar{y})^2 = \sum^n_{i=1}(\hat{y} - \bar{y})^2 + \sum^n_{i=1}\epsilon^2_i$
	{{ total variability = explained variability + unexplained variability }}