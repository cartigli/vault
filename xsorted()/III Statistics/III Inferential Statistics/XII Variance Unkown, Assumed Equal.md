go to 8 stores researching apple's cost
	assume variance is the same, so pool individual means and standard deviations
	[Pooled Variance] Formula:
		$s^2_p =  \frac{((n_x - 1)s^2_x (n_y - 1)s^2_y)}{n_x + n_y -2}$
				{only uses the sample size & variance}

| ny   | la   |
| ---- | ---- |
| 3.80 | 3.02 |
| 3.76 | 3.22 |
| 3.87 | 3.24 |
| 3.99 | 3.02 |
| 4.02 | 3.06 |
| 4.25 | 3.15 |
| 4.13 | 3.81 |
| 3.98 | 3.44 |
| 3.99 |      |
| 3.62 |      |
Calculate mean and stdev for each sample
	ny = $\bar{x} = 3.94, s = 0.18, n = 10$
	la = $\bar{x} = 3.25, s = 0.27, n = 8$
		$s^2_p =  \frac{((n_x - 1)s^2_x + (n_y - 1)s^2_y)}{n_x + n_y -2}$
		$s^2_p =  \frac{((10 - 1)0.18^2 + (8 - 1)0.27^2)}{10 + 8 - 2}$
		$s^2_p =  \frac{((9)0.18^2 + (7)0.27^2)}{16}$
		$s^2_p =  \frac{0.80}{16}$
		$s^2_p =  0.05$ [Pooled Variance]
		$\sqrt{s^2_p} =  \sqrt{0.05}$
		$s_p =  0.22$ [Pooled Standard Deviation]

Unknown variance, use t-stat & formula below
	$(\bar{x} - \bar{y}) \pm t_{n_x + n_y - 2, \alpha/2} \sqrt{\frac{s^2_x}{n_x} + \frac{s^2_y}{n_y}}$
	$(3.94 - 3.25) \pm t_{10 + 8 - 2, \frac{\alpha}{2}} \sqrt{\frac{0.05}{10} + \frac{0.05}{8}}$
	$(.69) \pm t_{16, \frac{\alpha}{2}} \sqrt{0.005 + 0.0063}$
	$(.69) \pm t_{16, .025} \sqrt{0.0113}$
	$(.69) \pm 2.12 * 0.11$
	$(.69) \pm 0.233$
	$(0.46, 0.92)$
		We are 95% confident that the actual difference between apple prices in NY and LA are between these intervals; apples in NY are more expensive than LA.