1. $5! = 1 \cdot 2 \cdot 3 \cdot 4 \cdot 5 = 120$
2. 8 graphics, 5 demographics
	a. 5 = p, demos to give ads to, 8 = n, elements avail
	variation without repetition
		$\bar{v}^n_p = n^p$
		$\bar{v}^8_5 = 8^5$
		$\bar{v}^8_5 = 32768$
	b. variation with repetition
		$\bar{v}^8_5 = \frac{n!}{p!}$
		$\bar{v}^8_5 = \frac{8!}{5!}$
		$\bar{v}^8_5 = 6 \cdot 7 \cdot 8$
		$\bar{v}^8_5 = 336$
	c. combinations without repetition
		$C^n_p = \frac{n!}{(n - p)! p!}$
		$C^8_5 = \frac{8!}{(8 - 5)! 5!}$
		$C^8_5 = \frac{8!}{(3)! 5!}$
		$C^8_5 = \frac{5 \cdot 6 \cdot 7 \cdot 8}{5!}$
		$C^8_5 = \frac{5 \cdot 6 \cdot 7 \cdot 8}{120}$
		$C^8_5 = \frac{1680}{120}$
		$C^8_5 = 14$
	d. combinations with repetition
		$C^n_p = \frac{(n + p - 1)!}{(n - 1)! p!}$
		$C^8_5 = \frac{(8 + 5 - 1)!}{(8 - 5)! 5!}$
		$C^8_5 = \frac{(12)!}{(3)! 5!}$
		$C^8_5 = \frac{4 \cdot 5 \cdot 6 \cdot 7 \cdot 8 \cdot 9}{5!}$
		$C^8_5 = \frac{4 \cdot 5 \cdot 6 \cdot 7 \cdot 8 \cdot 9}{120}$
		$C^8_5 = \frac{60480}{120}$
		$C^8_5 = 504$
\cdot
3. repainting each room, 2 bedrooms, kitchen, living room, bath, study, hall
	7 rooms; 9 colors of paint
	$n = 9, p = 7$
		a. every room a dif color:
			variations without repetition
			$\bar{v}^n_p = n^p$
			$\bar{v}^9_7 = 9^7$
			$\bar{v}^9_7  = 4,782,969$
		b. bath, study, hall white, so p - 3 = 4
		With variation now?
			$\bar{v}^n_p = \frac{n!}{p!}$
			$\bar{v}^9_4 = \frac{9!}{4!}$
			$\bar{v}^9_4 = \frac{5 \cdot 6 \cdot 7 \cdot 8 \cdot 9}{1}$
			$\bar{v}^9_4 = 15,120$
		without rep:
			$\bar{v}^n_p = n^p$
			$\bar{v}^9_4 = 9^4$
			$\bar{v}^9_4 = 6,561$
		c. same as above, but p - 2, not p - 3
		d. only use gray and yellow
		now, $n = 2, p = 7$
			~~~variation with repetition
			v.bar(n, p) = n! / p!
			v.bar(7, 2) = 2! / 7!
			v.bar(7, 2) = 2! / 7!~~~
			combinations with repetition ig
			$C^2_7 = \frac{(2 + 7 - 1)!}{(2 - 7)! \cdot 7!}$
			$C^2_7 ) = \frac{(2 + 7 - 1)!}{(-5)! \cdot 7!}$
			$C^2_7 =$ broken?
			7 rooms, each can be gray or yellow, 14 options

4, Career Fest [ maybe should be combinations without repetition ]
11 companies, room for all, n = 11 companies, p = 11 rooms
	assuming no preference in which room:
	permutations: 11!
	permutations: 39916800
	combo 
		$n = 11, p = 11$
		$C^n_p = \frac{n!}{(n - p)! \cdot p!}$
		$C^n_p  = \frac{11!}{(11 - 11)! \cdot 11!}$
		$C^n_p  =$ divide by 0 :(
only one has preference, for the middle:
	permutations: 10!
	permutations: 3628800
3 requests for the middle:
	8 random arrangements, 3 ordered
	$8! \cdot 3!$
	$241920$
One empty slot, so $n = 10, p = 11$
$C^n_p  = \frac{n!}{(n - p)! \cdot p!}$
$C^n_p = \frac{10!}{(10 - 11)! \cdot 11!}$
$C^n_p  = \frac{10!}{(-1)! \cdot 11!}$
breaks again?

	

2 5 minute chunks to do exercises with
3 for cardio 3n
5 legs options 5n
4 choices for 
- chest, shoulders, back 4n ,4n, 4n,
triceps, 2 options 2n
back, 2 options 2n
abs 4 options 4n

