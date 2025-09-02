P-value: Instead of testing at a predetermined confidence level, the P-Value is the smallest level of significance at which we can still reject the null hypothesis, given the observed sample statistic

Previous example:
	Standard Error: 2739
	Population Standard Deviation: 15000 [known]
	$N \sim (\mu, \sigma^2)$
		n = 30
				In the last example, the hypothesis of $\mu$ = 113,000 returned an associated Z-Score of -4.96, and was rejected with confidences of 95% and 99%
					What's the highest confidence, or P-Value, we could reject this null hypothesis at?
					p-value = 1 - lowest Z-score value [0.0001]
							compare the confidence level, $\alpha$
							90%; $\alpha$ is 0.1, 0.0001 < 0.1
							95%; $\alpha$ is 0.05, 0.0001 < 0.05
							99%; $\alpha$ is 0.01, 0.0001 < 0.01
						Honestly, this is a shit example, and the P-value seems essentially useless
			If the associated z-score was 2.12, which pointed to the value 0.9830, the associated P-Value would be 1 - 0.9830 = 0.017
					say its a two-sided test, the p-value is doubled and gets 0.034, so...
					$\alpha$ of 0.1 {90% confidence}, reject the null hypothesis
					$\alpha$ of 0.05 {95% confidence}, reject the null hypothesis
						$\alpha$ of 0.025 {99% confidence}, the null hypothesis cannot be rejected; 0.025 > 0.034, so the most confidence we could use to reject the null hypothesis would be between 95% and something like 97% {what do I look like, Einstein?}
							P-Value gives you the lowest z-score value that you can assign confidence to {you know what I mean}
							Closer to 0.000 the p-value is, the more confidence in your interval you can boast