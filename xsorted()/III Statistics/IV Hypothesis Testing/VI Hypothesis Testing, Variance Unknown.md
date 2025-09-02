Email Analysis; Estimate if our competitor has a higher open rate than our company
	Us: 40% of emails opened

Build the Test:
	$H_O = \mu_{or} \leq 40$%
	$H_A = \mu_{or} > 40$%
		Null $H_O$ says opposite of task because our job is to determine if they beating us, we're not 'hoping we are losing' here
			One sided test, only looking at greater than
			$\alpha$ = 0.05

Open Rate of Opposing Co.:
26%, 23%, 42%, 49%, 23%, 59%, 29%, 29%, 57%, 40%
	Sample Mean {$\bar{X}$}: 37.70 %
	Sample Standard Deviation {$\sigma$}: 13.74 %
	Standard Error {$\sigma / \sqrt{n}$}: 4.34 %
	Null Hypothesis value {$H_O$}: 40%
		Sample Size {n} & variance are unknown, so use the Student's t Distribution:
		~~~$CI = \bar{x} + or - t_{n-1,\alpha} * s / \sqrt{n}$
		$~~~CI = 37.70 \pm t_{10-1,0.05} * 13.74 / \sqrt{10}$
		$CI = 37.70 \pm t_{10-1,0.05} * 13.74 / \sqrt{10}$
		NOOOO~~~
		this is intervals, were hypothesis testing
				T = {$\bar{x} - \mu / s / \sqrt{n}$}
				T = {$37.70 - 40.00 / 13.74 / \sqrt{10}$}
				T = {$ -2.3 / 13.74 / 3.16$}
				T = {$ -2.3 / 4.34$}
				T = {$ -0.53$}
					With n - 1 {9} degrees of freedom, we get the T-score of 1.833 at the 5% significance the critical value
					T = 0.53 is less than t = 1.83
							Accept the Null if the value of the T-score is {<} LESS THAN the critical value t
							Reject the Null if the value of the T-score is GREATER THAN the critical value t
								We should accept the null hypothesis.
								We cannot say the opening rate of the client's emails is higher than 40%