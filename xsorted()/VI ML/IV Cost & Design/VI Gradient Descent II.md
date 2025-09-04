Our linear model : $y = x * w[eights] + b[iases]$
	every output $y_i$ is paired with an $x_i$ ; $y_i = x_i * w + b$
		*for house price given {info} model earlier, but applicable to all linear models*
			$x_i$ = information upon which to make the prediction of price
			$y_i$ = a single prediction given the input[s] of $x_i$
				$t_i$ = the corresponding target , given $x_i$
					we compare $t_i$ to $y_i$ to determine accuracy & Loss
						Loss is usually denoted as L(y,t) because those are its determimates
							*C(y,t) for Cost and E(y,t) for Error*

Linear Regression, so L2-Norm :
	$$\text{L2-Norm} = \sum(y_i - t_i)^2$$
	For our purposes : {{ division does not affect fundamentals of this Loss Function }}
	$$\frac{\text{L2-Norm}}{2} = \frac{\sum(y_i - t_i)^2}{2}$$
*reminders* :
	update rule:
		$x_{i+1} = x_i - \eta(f'(x_i))$
	