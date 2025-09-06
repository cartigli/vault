Dependent Samples: One sample depends on another's results
	Before and After comparisons
	Researching families; inherently interact and effect each other

Test with Confidence Intervals 
	Pop. variance known, 
	Pop. variance unknown but assumed equal
	Pop. variance unknown but assumed unequal

Detecting mg in blood:
	take two samples; one before and one after the pill is taken
		in biology/nature, assume natural variance, or Normal Distribution
		$N \sim (\mu, \frac{\sigma^2}{n})$

| b4   | After | Diff  |
| ---- | ----- | ----- |
| 2.00 | 1.70  | -0.30 |
| 1.40 | 1.70  | 0.30  |
| 1.30 | 1.80  | 0.50  |
| 1.10 | 1.30  | 0.20  |
| 1.80 | 1.70  | -0.10 |
| 1.60 | 1.50  | -0.10 |
| 1.50 | 1.60  | 0.10  |
| 0.70 | 1.70  | 1.00  |
| 0.90 | 1.70  | 0.80  |
| 1.50 | 2.40  | 0.90  |
		take differences, treat as 'New Sample'
				Find Mean & Standard Deviation of this new sample
Mean:
	$-0.30 +0.30 +0.50 +0.20 +-0.10 +-0.10 +0.10 +1.00 +0.80 +0.90$
	$\frac{3.30}{10 - 1}$
	$0.33$
	$(0.33-0.30)^2 +(0.30-0.33)^2 +(0.50-0.33)^2...$
	$\sigma = 0.45, n = 10$
		Formula for Confidence Interval for the Difference of two Samples = $\bar{d} \pm t_{n-1,\frac{\alpha}{2}} * \frac{s}{\sqrt{n}}$
		$\bar{d} \pm t_{n-1,\frac{\alpha}{2}} * \frac{s}{\sqrt{n}}$
		$0.33 \pm t_{10-1, 0.025} * \frac{0.45}{\sqrt{10}}$
		$0.33 \pm 2.26 * \frac{0.45}{\sqrt{10}}$
		$(0.01, 0.65)$
				"We are 95% confident the population mean will be within 0.01 and 0.65; 95% of the time the population mean will be within this interval."
			