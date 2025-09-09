biggest problem with data is magnitude - let's normalize it
standardization or feature scaling apply to regression ; normalization is ML

involves taking every value and subtracting the mean of the sample and dividing by the $\sigma$
standardized variable = $\frac{x - \mu}{\sigma}$

ex Euro - Dollar trade rate:

| day | exchange rate | daily trading volume |
| --- | ------------- | -------------------- |
| 1   | 1.3           | 110,000              |
| 2   | 1.34          | 98,700               |
| 3   | 1.25          | 135,000              |
exhange rate standardized:
		0.07
		0.96
		-1.03
daily trading standardized:
		-0.25
		-0.85
		1.1
					their vast differences in values are now much more succinct
					this allows for better handling of extreme differences and more sensible regression models