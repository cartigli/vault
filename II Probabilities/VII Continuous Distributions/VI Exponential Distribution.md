$Exp (\lambda)$
$X \sim Exp(1/2)$
	variable $x$ follows an exponential distribution with the scale of 1/2
	Usually starts high, decreases, and continues until it reaches a plateau
		approaching, but never reaching, 0
		PDF of this function follows the same, steep initial descent that plateaus at a low value, approaching 0
		CDF is similarly slopped, but opposite, approaching 1, starting at 0
Rate Limiter = $\lambda$
	defines how fast the curve of the CDF or PDF reaches the plateau
	or how spread out the graph is

$E(Y) = 1 / \lambda$
$Var(X) = 1 / \lambda^2$
	unlike Normal or Chi_squared Distributions, this has no known values
	transformation can be applied

$ln ( Y \sim Exp (\lambda) ) = X ~ N (\mu, \sigma^2)$
	used to run linear regressions; very common