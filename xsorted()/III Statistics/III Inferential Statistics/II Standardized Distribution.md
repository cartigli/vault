[Normalization] $\sim (\mu, \sigma^2) => \sim (0, 1)$
	$(x - \mu) / \sigma$
	if we normalize the $\sigma$ and the $\mu$ , we can get a z-score chart 

EX: og data: 1, 2, 2, 3, 3, 3, 4, 4, 5
	$1 + 2 + 3 + 3 + 3 + 4 + 4 + 5$
	$27 / 9$
	$3 = \mu$
		subtract $\mu$ from each data point and get a new $\mu$ @ 0
		-2, -1, -1, 0, 0, 0, 1, 1, 2
		$\mu$ = 0 [centered]
	
	$-2^2 + -1^2 + -1^2 + 0^2 + 0^2 + 0^2 + 1^2 + 1^2 + 2^2$
	$12 / 9 - 1$
	$S^2= 1.500$ [Variance]
	$S = 1.225$ [Standard Deviation]
		now, divide every data point by 1.22
		$-2/1.22, -1/1.22, -1/1.22, 0/1.22, 0/1.22, 0/1.22, 1/1.22, 1/1.22, 2/1.22$
		$-1.64, -0.82, -0.82, 0, 0, 0, 0.82, 0.82, 1.64$
		$-1.64^2 + -0.82^2 + -0.82^2 + 0 + 0 + 0 + 0.82^2 + 0.82^2 + 1.64^2$
		$2.69 + 0.67 + 0.67 + 0 + 0 + 0 + 0.67 + 0.67 + 2.69$
		$8.060 / 9 - 1$
		$\sigma= 1$ [rounding-errors]
			now, $X \sim N (0, 1)$	