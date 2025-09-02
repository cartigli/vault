single population and multiple populations
	variance is known test

data science salary
	mean is 100,200
	pop std 15,000
	std error 2739
	sample size 30
		someone suggests the average salary is 113,000
				two-sided test, rejecting the null {mean salary is 113,000} would be decided by the mean being over __or__ under 113
				$H_0 : \mu_0 = 113,000$
				$H_A : \mu_0 \neq 113,000$
	Note: *Z is the standard variable associated with the test called the [Z-score]
	*z is the value pulled from the Z-chart, i.e., 2.65, 1.96, etc., called the [Critical Value]*
		$Z \sim N (\bar{x} -\mu_0, 1)$
				Z is normally distributed over the mean of $\bar{x} - \mu_0$, with a standard deviation of one
					$Z = (\bar{x} - \mu_0)  / (\sigma / \sqrt{n})$
							^ formula to standardize a normal distribution
			$Z = (\bar{x} - \mu_0)  / (\sigma / \sqrt{n})$
			$Z = (100200 - 113,000)  / (2739)$
				100200 is the sample mean, the std-dev is known and 15,000, and $(\sigma / \sqrt{n})$ is the standard error, 2739
			$Z = (100200 - 113,000)  / (2739)$
			$Z = (-12800)  / (2739)$
			$Z = (-12800)  / (2739)$
			$Z = -4.673$
				Using an $\alpha$ of 0.05, or 95% confidence. Since it is a two tailed test, we divide the $\alpha$ by 2 and get the Z-scores
					0.05 / 2 = 0.025, and the associated z [Critical Value] is: 1.96
							4.67 > 1.96, so we reject $H_0$, the Null Hypothesis; or we reject this null hypothesis with 95% confidence
						We can test again with 99% confidence by comparing to the z-score of an $\alpha$ equal to 0.005 {divided by 2}
							the new associated z-score is 2.58, and 4.96 > 2.58, so with 99% confidence, we again reject the Null Hypothesis