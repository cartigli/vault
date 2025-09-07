$Po(\lambda)$
$Y \sim P_o (4)$
variable Y follows a poisson distribution with lambda ($\lambda$) equal to 4
	firefly might light 3 times in 10 seconds; use poisson to determine probability of it lighting up 8 times in 20 seconds
	Graphs events over time, so always starts at 0, because nothing could be, no event can happen 0 times
	Ex: usually, your students ask 4 questions a day, but today, it was 7
	P(y = 7) = what's the probability of your students asking exactly 7 questions?
		$\lambda = 4$, interval = 1 day, y = 7
		We need: $P_o(7)$
		$P(Y) = \frac{(\lambda)^{y} \cdot (e)^{-\lambda}}{y!}$
			e = Euler's number, Napier's constant; about 2.72
			$x^{-n} = \frac{1}{x^n} ; \text{ so } (e)^{-\lambda} = \frac{1}{(e)^{\lambda}}$
		$P(Y) = \frac{(4)^{7} \cdot (e)^{-4}}{7!}$
		$P(Y) = \frac{(16384) \cdot (0.0183)}{5040}$
		$P(Y) = \frac{299.83}{5040}$
		$P(Y) = 0.0595$
			the probability of your students asking exactly 7 questions in one day is 5.95%
			$E(Y) = \text{complex formula...}$
			$E(Y) = \lambda$
			$\mu = \sigma^2 = \lambda$ [mean & variance are both $\lambda$ in Poisson Distributions]