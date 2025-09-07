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
			$\sigma^2 = p (1 - p)$
			$\sigma = \sqrt{p (1 - p)}$
		Consider flipping an unfair coin that gets tails 60% of the time
			tails = 1
			heads = 0
			p(coin) = .6
				plug in to variance formula: $\sigma^2 = p \cdot (1 - p); \sigma = \sqrt{p \cdot (1 - p)}$
				$\sigma = \sqrt{.6 \cdot (1 - .6)}$
				$\sigma = .48989$
				$\sigma^2 = .24$