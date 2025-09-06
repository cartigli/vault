Same as Z-Score normal distribution, but fatter tails to accommodate for less known about the population's variance
[Student T Distribution] : $t_{n-1, \alpha} = \bar{x} - \frac{\mu}{(\frac{s}{\sqrt{n}})}$
	Usually n-1 degrees of freedom; t
		Just like z-score, we have a chart for common confidence intervals 
			After 30 samples, it is essentially a z-score
			If 50 or more samples, use Z-score
			If 50 or less samples, use t-Statistic

Looking for mean data scientist salary:
	do not have pop. variance, only 9 samples available 

| 78,000  |
| ------- |
| 90,000  |
| 75,000  |
| 117,000 |
| 105,000 |
| 96,000  |
| 89,500  |
| 102,300 |
| 80,000  |
Sample mean = 92,533
Sample Standard Deviation = 13,932
Sample Standard Error = 4,644
		$CI = \bar{X} + or - t_{n-1,\frac{\alpha}{2}} * \frac{\sigma}{\sqrt{n}}$
		$CI = 92,533 + or - t_{9-1,0.05/2} * \frac{4,644}{\sqrt{9}}$
		$CI = 92,533 + or - t_{8,0.025} * \frac{4,644}{3}$
		$CI = 92,533 + or - 2.31 * \frac{4,644}{3}$
		$CI = 92,533 + or - 2.31 * 1,548$
		$CI = 92,533 + or - 3,474.88$
		$CI = 92,533 + or - 3,474.88$
		$CI = (88957.12, 96108.88)$