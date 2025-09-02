When we have a sample mean of $\bar{X}$ which is normally distributed around $\bar{X}$, we're saying:
	we are 95% confident that the population mean, $\mu$, will be within one standard deviation of the Sample Mean, $\bar{X}$
		There is a 2.5% chance $\mu$ will be on the right of the interval, and a 2.5% chance that $\mu$ will fall on the left of the interval
			overall, there is a 5% chance that $\mu$ will be outside of one standard deviation from $\bar{X}$

```mermaid
xychart-beta
  title "Confidence Interval"
  x-axis "outcome" ["2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12"]
  y-axis "probability" 0 --> 10
  bar [.1, 1, 3, 4, 6, 7, 6, 4, 3, 1, .1]
  ```
  We can say 7 is our $\bar{X}$, and Z and -Z would be at 10 and 4, respectively
			with 95% confidence and a Z-score of 1.96, the upper and lower limits are -1.96 and 1.96 on the [Normalized Standard Distribution Curve]
			CI =$\bar{X} + or - Z_\alpha/2 * \sigma / \sqrt{n}$
				As Confidence increases, i.e., 90% to 99%, the interval increases to fit the confidence
				As Confidence decreases, the interval decreases but is less insightful

For T-Distributions, use this formula
	CI =$\bar{X} + or - t_{n-1,\alpha/2} * s / \sqrt{n}$
	