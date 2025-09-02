Two classes' grades, engineering and management: Independent

|       | Engineering | Management |
| ----- | ----------- | ---------- |
| Size  | 100         | 70         |
| Mean  | 56          | 65         |
| Stdev | 10          | 5          |
Asummed normal distribution, samples are large, and variance is known
	use Z Stat
	Variance of the Difference formula:
		$\sigma^2_{diff} = \sigma^2_e / n_e + \sigma^2_m / n_m$
		$\sigma^2_{diff} = 100 / 100 + 25 / 70$
	Confidence Interval for two Independent Samples:
		$(\bar{x} - \bar{y}) \pm z_{\alpha/2} \sqrt{\sigma^2_x / n_x + \sigma^2_y / n_y}$
		$(56 - 65) \pm 1.96 \sqrt{10 + .357}$
		$(56 - 65) \pm 1.96 * 3.22$
		$(-9) \pm 6.30$
		$(-15.3, -2.69)$
				"We are 95% confident that the true mean difference between Engineering and Management falls into this interval."
					The negative bounds = Engineers constantly got lower grades than Management