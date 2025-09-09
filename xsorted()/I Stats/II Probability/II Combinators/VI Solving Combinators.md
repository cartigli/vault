variation can double count combinations
hiring manager looking to hire 3 people, A, B, & C, of 10
- choosing A, B, & C is the same as choosing C, B, & A
- *different variations, but not different combinations

Permutations - P(n) elements = n!
- $P(\text{who to hire}) = 6 (1 \cdot 2 \cdot 3)$
- 6 variations for Any combination
		6 times fewer combinations than variations, or 6 times more variations than combinations

Variations $\bar{v}^10n_3p = \frac{10!}{(10 - 3)!} = 8 \cdot 9 \cdot 10 = 720 \text{ variations}$

Combinations $C^10n_3p = \frac{720}{6} = 120$ [no double counting]

We can say all the different permutations of a single combination are different variations
Permutations = 6, Combinations = 120, Variations = 720

How many combinations can be made form P-many elements out of a sample of N elements?
Number of combinations = Number of variations / Number of permutations
$C^n_p = \frac{V^n_p}{P^n_p}$
$C^n_p = \frac{n!}{p! (n-p)!}$
	$C^{10}_3 = \frac{10!}{3! (10 - 3)!}$
	$C^{10}_3 = \frac{10!}{3! (7)!}$
	$C^{10}_3 = \frac{8 * 9 * 10}{1 * 2 * 3}$
	$C^{10}_3 = \frac{720}{6} = 120$

What if 4 clients were picked, not 3?
$C^{10}_4 = \frac{10!}{4! (10 - 4)!}$
$C^10_4 = \frac{10!}{4! (6)!}$
$C^10_4 = \frac{7 \cdot 8 \cdot 9 \cdot 10}{4!}$
$C^10_4 = \frac{7 \cdot 8 \cdot 9 \cdot 10}{1 \cdot 2 \cdot 3 \cdot 4}$
$C^10_4 = \frac{5040}{24}$
$C^10_4 = 210$

how many combos of 3 macs can you get w 8 flavors
$n = 8, p = 3$
$C^8_3 = \frac{8!}{3! (8-3)!}$
$C^8_3 = \frac{8!}{3! (5)!}$
$C^8_3 = \frac{6 \cdot 7 \cdot 8}{3!}$
$C^8_3 = \frac{6 \cdot 7 \cdot 8}{1 \cdot 2 \cdot 3}$
$C^8_3 = \frac{336}{6}$
$C^8_3 = 56$ possible combinations [without repeating]

$n = 8, p = 5$
$C^8_3 = \frac{8!}{5! (8-5)!}$
$C^8_3 = \frac{8!}{5! (3)!}$
$C^8_3 = \frac{4 \cdot 5 \cdot 6 \cdot 7 \cdot 8}{5!}$
$C^8_3 = \frac{4 \cdot 5 \cdot 6 \cdot 7 \cdot 8}{1 \cdot 2 \cdot 3 \cdot 4 \cdot 5}$
$C^8_3 = \frac{6720}{120}$
$C^8_3 = 56 \text{ possible combinations}$

$n = 8, p = 8$
$C^8_8 = \frac{8!}{8! (8-8)!}$
$C^8_8  = \frac{8!}{8!}$
$C^8_8  = 1$