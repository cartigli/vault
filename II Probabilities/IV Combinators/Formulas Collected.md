n = sample of elements, p = positions to fill

[Permutations]
	permutations = ways to arrange set of n elements
	 P = n!

[Variations] order and arrangement matter
	Without repetition:
		v.bar(n, p) = n! / (n - p)!
	with repetition:
		v.bar(n, p) = n^p

[Combinations] order and arrangement don't matter
	without repetition:
		$C^{n}_p$ = n! / (n - p)! p!
	with repetition:
		C(n, p) = (n + p - 1)! / (n - 1)! p!

C(n, p) = V [variations] / P [permutations]