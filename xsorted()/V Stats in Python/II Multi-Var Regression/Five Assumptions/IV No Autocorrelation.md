AKA no serial correlation
$\sigma_{\epsilon_i \epsilon_j} = 0 : \forall i \neq j$
		errors are assumed to be uncorrelated.
						if some unknown bias is present, like every 5th n is down and every 10th is up, the regression model does not consider this
			one way to determine if this issue is present is the Durbin-Watson Test, which is on the OLS report
					it falls between 0 and 4
					scoring 2 means no autocorrelation
					scoring below 1 or over 3 would be cause for alarm
									also, if you threw the independent variables on a scatter plot and could find a pattern, there is probably autocorrelation present

un-relaxable, if present must purge or avoid, 
	cannot remedy or improve