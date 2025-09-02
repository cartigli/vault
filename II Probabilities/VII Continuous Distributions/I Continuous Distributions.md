Sample Space = infinite
	can't represent with table, have to move to graph
	denoted with f(y) = associated probability for every possible value; y
		Since more values in sample space, bars from discrete distributions become infinetly small, form a curve called the Probability Distribution Curve

P(y) = favorable / all
	for continuous, all = infinite, and almost all values get very, very close to 0, insignificant, probability basically is 0
	so, probability of any given value from a continuous distribution is essentially 0
		Ex: probability of a college runner runnning a race in under 6 minutes is the same as them running it for atleast 6 minutes; them finishing in exactly 6 has the probability of 0

Cumulative Distribution Function (CDF)
Everything leading up to a value, F(y)
	Calculates probability of a certain value to be at or below a specific value
	no value can be less than -$\infty$ F(-$\infty$) = 0, and F($\infty$) = 1
	Useful for probabilities over intervals
		do this by finding the integral of the density curve from points a to b
		$\int^a_b p(x)dx$
			For example, the probability of the interval: (-$\infty$; y) is $\int^{y}_{-\infty} p(y)dy = F(y)$
			PDF $\int$ = CDF : $\int^{y}_{-\infty} p(y)dy = F(y)$
			CDF (derivative) = PDF : p(y) = F(y)d/dy

Usually, only given PDF, compute: 
	E(y) = ?
	Var(y) = ?
		P(y) = 0 for continuous distributions, so can't use summation
		E(y) = integral of the product of any element y and its associated pdf value, over the variables -infinity to infinity
		E(y) = $\int^{-\infty}_\infty yp(y)dy$
		$Var(y) = E(y^2) - E(y)^2$
		