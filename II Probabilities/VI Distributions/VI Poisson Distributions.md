Po($\lambda$)
Y ~ P o (4)
variable Y follows a poisson distribution with lambda ($\lambda$) equal to 4
	firefly might light 3 times in 10 seconds; use poisson to determine probability of it lighting up 8 times in 20 seconds
	Graphs events over time, so always starts at 0, because nothing could be, no event can happen 0 times
	Ex: usually, your students ask 4 questions a day, but today, it was 7
	P(y = 7) = what's the probability of your students asking exactly 7 questions?
		$\lambda$ = 4, interval = 1 day, y = 7
		We need: P o (7)
		P(Y) = $(\lambda)^{y} (e)^{-\lambda} / y!$
			e = euler's number, Napier's constant; about 2.72
			$x^{-n} = 1 / x^n ; so (e)^{-\lambda} = 1 / (e)^{\lambda}$
		P(Y) = $(4)^{7} (e)^{-4} / 7!$
		P(Y) = $(16384) (0.0183) / 5040$
		P(Y) = $299.83 / 5040$
		P(Y) = $0.0595$
			the probability of your students asking exactly 7 questions in one day is 5.95%
			E(Y) = complex formula...
			E(Y) = $\lambda$
			$\mu = \sigma^2 = \lambda$ [mean & variance are both $\lambda$ in Poisson Distributions]