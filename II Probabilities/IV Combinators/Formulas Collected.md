n = sample of elements, p = positions to fill

[Permutations]
	permutations = ways to arrange set of n elements
	 $P = n!$

[Variations] order and arrangement matter
	Without repetition:
		$\bar{v}(n, p) = \frac{n!}{(n - p)!}$
	with repetition:
		$\bar{v}(n, p) = n^p$

[Combinations] order and arrangement don't matter
	without repetition:
		$C^{n}_p = \frac{n!}{(n - p)! p!}$
	with repetition:
		$C^n_p = \frac{(n + p - 1)!}{(n - 1)! p!}$

$C^n_p = \frac{V [variations]}{P [permutations]}$