Logistic ($\mu$, S) (S=scale parameter $\mu$ is the location param)
$Y \sim Logistic (6, 3)$
	variable Y follows a logistic Distribution with location 6 and a scale of 3
	mostly + or - outputs; forecasting victory or defeat
	Ex: determining if a tennis serve's speed effects the outcome of the match [win or lose]
		one would assume as speed increases, the opponents reaction time is diminished, increasing the chance of victory
		in reality, as serves gain speed, innacuracy of the shot increases, resulting in more defaults by the server
			theory suggests there exists an optimal speed; and decreasing or inceasing beyond this decreases the probability of a point scored or match won
			expanding this, we would assume the PDF of the Logistic Distribution would be similar to that of a Normal Distribution; a bell curve
	Graphs of the Logistic Distribution are based on:
		mean: $\mu$
			dictates the center of the graph
		and the scale parameter: $S$
			dictates how spread the graph is
				For tennis example, $\mu$ = optimal serve speed, and $S$ = variations in speed with decrease in accuracy
	CDF = starts slow, picks up quickly, and plateaus near 1
		in tennis example, graph's curve at $\mu$ is much steeper at x = $\mu$ because the shots' effectiveness is at its maximum here, so summing them all up means this is the steepest portion of the graph
			As S increases, so does the point of 'pick up' on the graph, and the point at which it plateaus approaching 1 decreases

E(Y) = $\mu$
Var(Y) = $(S^2 * \pi^2) / (3)$
