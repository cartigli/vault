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
		Probability of getting a given outcome a precise number of times over n trials, use the $p(y) fx$
			Each trial is a Bernoulli Event [one trial, two possibilities]
				P (desired outcome) = p,
				P (alternative outcome) = 1 - p
				To get the desired output exactly y-many times over the n trials, 
				we also need to know n - y
					if we didn't, the obtained probability would be getting the desired output *atleast* y-many times
					Also multiple ways to get desired outcome, so we use combinations
						The number of ways in which 4 out of the 6 trials could be successful is equal to the combinations of 4 elements out of a sample space of 6
						$C^4_6; \text{ so } C^y_n$ is what we need
						Three ways to get tails exactly twice in three trials
							$C^2_3$
									H T T
									T H T
									T T H
							$p(y) = (\text{picking y elements from n trials}) \cdot p^y \cdot (1 - p)^{n-y}$
							$p(y) = C^n_y * p^y \cdot (1 - p)^{n-y}$
						Ex: General Motors Single Stock
							$p(\text{up}) = 60$%
							$p(\text{down}) = 40$%
						How many days will the stock price increase out of 5 days?
							$p(y) = \text{probability of stock up}$
							$n = 5 \text{ days}$
							$y = 3$
							$p(y) = C^5_3 \cdot p^y \cdot (1 - p)^{n-y}$
							$p(y) = C^5_3 \cdot .6^3 \cdot (1 - .6)^{5-3}$
							$p(y) = C^5_3 \cdot .216 \cdot (.4)^{2}$
							$p(y) = C^5_3 \cdot .216 \cdot .16$
							$p(y) = C^5_3 \cdot 0.03456$
							$p(y) = C^5_3 \cdot 0.03456$
								$C^{n}_p$ = $\frac{n!}{(n - p)! \cdot p!}$
								$C^{n}_p$ = $\frac{5!}{(5 - 3)! \cdot 3!}$
								$C^{n}_p$ = $\frac{3 \cdot 4 \cdot 5}{3!}$
								$C^{n}_p$ = $\frac{3 \cdot 4 \cdot 5}{1 \cdot 2 \cdot 3}$
								$C^{n}_p$ = $\frac{60}{6}$
								$C^{n}_p$ = 10
							$p(y) = C^5_3 \cdot 0.03456$
							$p(y) = 10 \cdot 0.03456$
							$p(y) = 0.3456$
								so, we have a 34.56% chance of getting exactly 3 increases in stock price over 5 days
		Expected Values = sum of all values in a sample space multiplied by their respective probabilities
			$E(Y) = p \cdot n$
				variance formula
				$\sigma^2 = E(Y)^2 - E(y)^2$
				$\sigma^2 = n \cdot p \cdot (1 - p)$
				$\sigma^2 = 5 \cdot .6 \cdot (1 - .6)$
				$\sigma^2 = 1.2$
				$\sigma = \sqrt{1.2}$