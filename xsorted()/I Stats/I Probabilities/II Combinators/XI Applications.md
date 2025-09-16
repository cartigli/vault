Ordering from restaurant 
1. Deals
		1 person combo pack
			medium pizza, small drink, dessert
		family deal
			2 med pizzas, 2 drinks (one small, one large), 2 desserts
		double delight
			2 med pizzas, 2 L drinks, 2 desserts
26 pizzas, 4 drinks, 7 types of deserts

1 person combo:
	pizza, small drink, dessert
	26, 4, 7
Combinations $= 26 \cdot 4 \cdot 7 = 728$ ways to combine

family deal: 2 pizzas, 2 drinks(one small, one large), 2 desserts; 26, 4, 7
Combinations without Repetition; pick p-many elements from n sample
	$n = 26, p = \frac{2}{4}$
	$C^{26}_2 = \frac{26!}{(26-2)! 2!}$
	$C^{26}_2 = \frac{26!}{(24)! 2!}$
	$C^{26}_2 = \frac{25 \cdot 26}{1 \cdot 2}$
	$C^{26}_2 = \frac{650}{2}$
	$C^{26}_2 = 325 \text{ combinations for pizza}$
Drinks:
Variations [with repetition] n = total elements [4], p = slots [2], $\bar{v} = n^p$
	$\bar{v} = 4^2$
	$\bar{v} = 16$
Desserts:
Combinations with Repetition $= C^n_p = \frac{(n + p - 1)!}{(n - 1)! p!}$
	$n = 7, p = 2$
	$C^7_2 = \frac{(7 + 2 -1)!}{(7 - 1)! 2!}$
	$C^7_2 = \frac{8!}{(6)! 2!}$
	$C^7_2 = \frac{7 \cdot 8}{1 \cdot 2}$
	$C^7_2 = \frac{56}{2}$
	$C^7_2 = 28$
Ways to combine $= 325 \cdot 16 \cdot 28 = 145,600 \text{ different ways of combining}$

Family Deal:
Same calculations for Pizza & Desserts, Drinks now can't repeat
Pizzas: 325 options
Desserts: 28 options
Drinks; Variations without repetition; n = options, p = slots to fill
	$\bar{v}^n_p = \frac{n!}{p!}$
	$\bar{v}^4_2 = \frac{4!}{2!}$
	$\bar{v}^4_2 = \frac{3 * 4}{1}$
	$\bar{v}^4_2 = 12$
Combinations $= 325 \cdot 12 \cdot 28 = 109,200$