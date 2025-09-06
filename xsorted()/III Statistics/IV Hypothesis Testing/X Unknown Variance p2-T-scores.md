Independent samples, unknown variances assumed equal
testing apple prices in LA vs NY
	don't know variance; assumed equal
null hypothesis is the mean price in ny is equal to la
	$H_0 : \mu_{ny} - \mu_{la} = 0$
	$H_A : \mu_{ny} - \mu_{la} \neq 0$

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
$ny: \frac{39.41}{10} = 3.94$
	Stddev: 0.18
$la: \frac{25.96}{8} = 3.25$
	0.27

$s^2_p = \frac{(n_x - 1)s^2_x + (n_y - 1)s^2_y}{n_x + n_y -2}$
$s^2_p = \frac{(10 - 1)0.18^2 + (8 - 1)0.27^2}{10 + 8 - 2}$
$s^2_p =  \frac{(9)0.18^2 + (7)0.27^2}{16}$
$s^2_p = \frac{(9)0.0324 + (7)0.0729}{16}$
$s^2_p = \frac{0.2916 + .5103}{16}$
$s^2_p =  \frac{0.8019}{16}$
$s^2_p = 0.0501$ = Pooled Variance
	Pooled STD DEV is variance over the n's squared:
	$\sqrt{\frac{0.05}{10} + \frac{0.05}{8}}$
	$\sqrt{0.005 + 0.00625}$
	$\sqrt{0.01125}$
	$0.106$ = the Pooled Standard Deviation
		$t_{n-1, \alpha} = \frac{\bar{x} - \mu}{ST.err}$
		$t_{n-1, \alpha} = \frac{(3.94-3.25) - 0}{0.11}$
		$t_{n-1, \alpha} =  \frac{0.69}{0.11}$
		$t_{10+8-2, \alpha} =  6.27$
				With t or z values over 4-5, the associated p-value is essentially 0, or 0.0001, with the three 0's signifying extreme significance
				the associated p-value for t=6.27 is p=0.0001
				since 0.0001 is lower than almost any confidence value we could set, we reject the Null Hypothesis with any and all common and many uncommon levels of significance