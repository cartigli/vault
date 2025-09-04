Our linear model : $y = x * w[eights] + b[iases]$
	every output $y_i$ is paired with an $x_i$ ; $y_i = x_i * w + b$
		*for house price given {info} model earlier, but applicable to all linear models*
			$x_i$ = information upon which to make the prediction of price
			$y_i$ = a single prediction given the input[s] of $x_i$
				$t_i$ = the corresponding target , given $x_i$
					we compare $t_i$ to $y_i$ to determine accuracy & Loss
						Loss is usually denoted as L(y,t) because those are its determinates
							*C(y,t) for Cost and E(y,t) for Error*

Linear Regression, so L2-Norm :
	$$L(y,t)=\text{L2-Norm} = \sum(y_i - t_i)^2$$
	For our purposes : {{ division does not affect fundamentals of this Loss Function }}
	$$\frac{\text{L2-Norm}}{2} = \frac{\sum(y_i - t_i)^2}{2}$$
*reminders* :
	Learning Rate
		$\eta$
	update rule:
		$$x_{i+1} = x_i - \eta(f'(x_i))$$
		becomes:
									$$w_{i+1} = w_i - \eta * \triangledown_w * L(y,t))$$
				& :
$$b_{i+1} = b_i - \eta * \triangledown_b * L(y,t))$$

$\triangledown_w$ = gradient of the loss function, with respect to $w_{weights}$
$\triangledown_b$ = gradient of the loss function, with respect to $b_{biases}$
		$\triangledown_w , \triangledown_b$ are our model's Optimization Functions
			the goal of our model is to lower this function through adjustment of weights and biases

$\triangledown_w L = \sum_i \triangledown_w \frac{1}{2} (y_i - t_i)^2$
' the loss gradient in respect to weights of the Loss Function are equal to the sum of the gradients 1/2 times $y_i - t_i$ squared in respect to weights '
	the $y_i$ is from $y_i = x_i*w + b$ , so plugging in these values for $y_i$ , we get :
		$=\sum_ix_i(y_i-t_i) =$
			because w & b are constants, so they become 0, and x is linear, so it becomes a scalar and can be simply distributed among the contents of the parenthesis
		it can also be helpful to combine $(y_i-t_i)$ into a single variable ; delta
			$\delta = (y_i-t_i)$
				$\delta$ *is often used to denote differences

$\triangledown_w L = \sum_i x_i \delta_i$
$\triangledown_b L = \sum_i \delta_i$
Now can be plugged into Optimization Functions:
$$w_{i+1} = w_i - \eta * \triangledown_w * L(y,t))\text{ becomes :}$$
$$w_{i+1} = w_i - \eta * \sum_i x_i \delta_i$$
				& :
$$b_{i+1} = b_i - \eta * \triangledown_b * L(y,t))\text{ becomes :}$$
$$b_{i+1} = b_i - \eta * \sum_i \delta_i$$
*I did not understand any of this , nor the deeper look provided, until I discovered that this simplification is the **partial derivative**.*
$\triangledown_w L = \sum_i \triangledown_w \frac{1}{2} (y_i - t_i)^2$
$\triangledown_w L = \sum_i \triangledown_w \frac{1}{2} ((xw+b) - t_i)^2$
$\triangledown_w L = \triangledown_w \frac{1}{2} \sum_i (xw + b - t_i)^2$


$$\nabla_w \sum_i f_i = \sum_i \nabla_w f_i$$

$$\nabla_w \frac{1}{2} \sum_i f_i = \frac{1}{2} \nabla_w \sum_i f_i = \frac{1}{2} \sum_i \nabla_w f_i = \sum_i \nabla_w \frac{1}{2} f_i$$