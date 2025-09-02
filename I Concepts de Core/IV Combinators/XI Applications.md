Ordering from restaurant 
1. Deals
		1 person combo pack
			medium pixxa, small drink, dessert
		family deal
			2 med pizzas, 2 drinks (one small, one large), 2 desserts
		double delight
			2 med pizzas, 2 L drinks, 2 desserts
26 pizzas, 4 drinks, 7 types of deserts

1 person combo:
	pizza, small drink, dessert
	26, 4, 7
Combinations = 26 x 4 x 7 = 728 ways to combine

family deal: 2 pizzas, 2 drinks(one small, one large), 2 desserts; 26, 4, 7
Combinations without Repetition; pick p-many elements from n sample
	n = 26, p = 2
	C(26, 2) = 26! / (26-2)! 2!
	C(26, 2) = 26! / (24)! 2!
	C(26, 2) = 25 x 26 / 1 x 2
	C(26, 2) = 650 / 2
	C(26, 2) = 325 combinations for pizza
Drinks:
Variations [with repetition] n = total elements [4], p = slots [2], V{bar} = n^p
	$\bar{V}$ = $4^2$
	$\bar{V}$ = 16
Desserts:
Combinations with Repetition = C(n, p) = (n + p - 1)! / (n - 1)! p!
	n = 7, p = 2
	C(7, 2) = (7 + 2 -1)! / (7 - 1)! 2!
	C(7, 2) = (8)! / (6)! 2!
	C(7, 2) = 7 x 8 / 1 x 2
	C(7, 2) = 56 / 2
	C(7, 2) = 28
Ways to combine = 325 x 16 x 28 = 145,600 different ways

Family Deal:
Same calculations for Pizza & Desserts, Drinks now can't repeat
Pizzas: 325 options
Desserts: 28 options
Drinks; Variations without repetition; n = options, p = slots to fill
	$\bar{V}$(n, p) = n! / p!
	$\bar{V}$(4, 2) = 4! / 2!
	$\bar{V}$(4, 2) = 3 x 4 / 1
	$\bar{V}$(4, 2) = 12
Combinations = 325 x 12 x 28 = 109200