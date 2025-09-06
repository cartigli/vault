[Uniform Distribution]
$U (a, b)$
$X \sim U (3, 7)$ is read as:
	variable x follows a discrete Uniform Distribution over the intervals 3, 7
		all outcomes have equal probabilities; rolling a dye
		when all outcomes have equal probabilities, Expected outcomes are useless
			mean and variance are uninterpretable

[Bernoulli Distribution]
$Bern (p)$
$X \sim Bern (p)$
	variable x follows a discrete Bernoulli Distribution with a probability of success equal to p
		Events that follow the bernoulli distribution are ones that have *one trial*, and *two outcomes*
		A single coin flip, one true or false question, etc.; either have past data or P(p) is known
		graph is two bars, one for each outcome
			one rises on y axis to p
			one goes on x axis to -p
				assign a 0 or a 1 to events
				lower prob = 1 - p
				higher prob = p
			$\sigma^2$ = p (1 - p)
			$\sigma$ = $\sqrt{p (1 - p)}$
		Consider flipping an unfair coin that gets tails 60% of the time
			tails = 1
			heads = 0
			p(coin) = .6
				plug in to variance formula: $\sigma^2$ = p (1 - p); $\sigma$ = $\sqrt{p (1 - p)}$
				$\sigma$ = $\sqrt{.6 (1 - .6)}$
				$\sigma$ = .48989
				$\sigma^2$ = .24

[Binomial Distribution]
$B (n, p)$
$X \sim B (10, 0.6)$
	variable x follows a binomial distribution across 10 trials and a likelihood of .6 to succeed on each trial
	$Bern (p) = B (1, p)$
		Suppose a pop quiz is given, with 10 T / F Questions
		Guessing one question is a Bernoulli event; Guessing them all is a Binomial event
			Expected value of Bernoulli event is the outcome we expect for a single trial
			Expected value of a Binomial event is the number of times we expect to get a specific outcome
		Flipping the unfair coin:
			The graph of this distribution would be n+1 bars wide, n= number of trials 
			If we toss the coin twice, we need three bars for all outcomes; 0, 1, & 2
				0 = no success out of 2, 1 = one success out of two, 2 = all trials success out of 2
		Probability of getting a given outcome a precise number of times over n trials, use the p(y) fx
			Each trial is a Bernoulli Event [one trial, two possibilities]
				P (desired outcome) = p,
				P (alternative outcome) = 1 - p
				To get the desired output exactly y-many times over the n trials, 
				we also need to know n - y
					if we didn't, the obtained probability would be getting the desired output *atleast* y-many times
					Also multiple ways to get desired outcome, so we use combinations
						The number of ways in which 4 out of the 6 trials could be successful is equal to the combinations of 4 elements out of a sample space of 6
						C (4, 6); so C (y, n) is what we need
						Three ways to get tails exactly twice in three trials
							C (2, 3)
									H T T
									T H T
									T T H
							p(y) = (picking y elements from n trials) x $p^y$ x $(1 - p)^(n-y)$
							p(y) = $C^{n}_y$ x $p^y$ x $(1 - p)^{n-y}$
						Ex: General Motors Single Stock
							p(up) = 60%
							p(down) = 40%
						How many days will the stock price increase out of 5 days?
							p(y) = probability of stock up
							n = 5 days
							y = 3
							p(y) = $C^{5}_3$ x $p^y$ x $(1 - p)^{n-y}$
							p(y) = $C^{5}_3$ x $.6^{3}$ x $(1 - .6)^{5-3}$
							p(y) = $C^{5}_3$ x $.216$ x $(.4)^{2}$
							p(y) = $C^{5}_3$ x $.216$ x $.16$
							p(y) = $C^{5}_3$ x $0.03456$
							p(y) = $C^{5}_3$ x $0.03456$
								$C^{n}_p$ = $\frac{n!}{(n - p)! p!}$
								$C^{n}_p$ = $\frac{5!}{(5 - 3)! 3!}$
								$C^{n}_p$ = $\frac{3 x 4 x 5}{3!}$
								$C^{n}_p$ = $\frac{3 x 4 x 5}{1 x 2 x 3}$
								$C^{n}_p$ = $\frac{60}{6}$
								$C^{n}_p$ = 10
							p(y) = $C^{5}_3$ x $0.03456$
							p(y) = $10$ x $0.03456$
							p(y) = $0.3456$
								so, we have a 34.56% chance of getting exactly 3 increases in stock price over 5 days
		Expected Values = sum of all values in a sample space multiplied by their respective probabilities
			E(Y) = p x n
				variance formula
				$\sigma^2 = E(Y)^2 - E(y)^2$
				$\sigma^2 = n * p * (1 - p)$
				$\sigma^2 = 5 * .6 * (1 - .6)$
				$\sigma^2 = 1.2$
				$\sigma = \sqrt{1.2}$
				