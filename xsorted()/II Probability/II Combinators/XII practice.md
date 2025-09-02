1. 5! = 1 x 2 x 3 x 4 x 5 = 120
2. 8 graphics, 5 demographics
	a. 5 = p, demos to give ads to, 8 = n, elements avail
	variation without repetition
		v.bar(n, p) = n^p
		v.bar(8, 5) = 8^5
		v.bar(8, 5) = 32768
	b. variation with repetition
		v.bar(8, 5) = n! / p!
		v.bar(8, 5) = 8! / 5!
		v.bar(8, 5) = 6 x 7 x 8
		v.bar(8, 5) = 336
	c. combinations without repetition
		C(n, p) = n! / (n - p)! p!
		C(8, 5) = 8! / (8 - 5)! 5!
		C(8, 5) = 8! / (3)! 5!
		C(8, 5) = 5 x 6 x 7 x 8 / 5!
		C(8, 5) = 5 x 6 x 7 x 8 / 120
		C(8, 5) = 1680 / 120
		C(8, 5) = 14
	d. combinations with repetition
		C(n, p) = (n + p - 1)! / (n - 1)! p!
		C(8, 5) = (8 + 5 - 1)! / (8 - 5)! 5!
		C(8, 5) = (12)! / (3)! 5!
		C(8, 5) = 4 x 5 x 6 x 7 x 8 x 9 / 5!
		C(8, 5) = 4 x 5 x 6 x 7 x 8 x 9 / 120
		C(8, 5) = 60480 / 120
		C(8, 5) = 504

3. repainting each room, 2 bedrooms, kitchen, living room, bath, study, hall
	7 rooms; 9 colors of paint
	n = 9, p = 7
		a. every room a dif color:
			variations without repetition
			v.bar(n, p) = n^p
			v.bar(9, 7) = 9^7
			v.bar(9, 7) = 4782969
		b. bath, study, hall white, so p - 3 = 4
		With variation now?
			v.bar(n, p) = n! / p!
			v.bar(9, 4) = 9! / 4!
			v.bar(9, 4) = 5 x 6 x 7 x 8 x 9 / 1
			v.bar(9, 4) = 15120
		without rep:
			v.bar(n, p) = n^p
			v.bar(9, 4) = 9^4
			v.bar(9, 4) = 6561
		c. same as above, but p - 2, not p - 3
		d. only use gray and yellow
		now, n = 2, p = 7
			~~~variation with repetition
			v.bar(n, p) = n! / p!
			v.bar(7, 2) = 2! / 7!
			v.bar(7, 2) = 2! / 7!~~~
			combinations with repetition ig
			C(2, 7) = (2 + 7 - 1)! / (2 - 7)! 7!
			C(2, 7) = (2 + 7 - 1)! / (-5)! 7!
			C(2, 7) = broken?
			7 rooms, each can be gray or yellow, 14 options

4, Career Fest [ maybe should be combinations without repetition ]
11 companies, room for all, n = 11 companies, p = 11 rooms
	assuming no preference in whoch room:
	permutations: 11!
	permutations: 39916800
	combo 
		n = 11, p = 11
		C(n, p) = n! / (n - p)! p!
		C(n, p) = 11! / (11 - 11)! 11!
		C(n, p) = divide by 0 :(
only one has preference, for the middle:
	permutations: 10!
	permutations: 3628800
3 requests for the middle:
	8 random arrangements, 3 ordered
	8! x 3!
	241920
One empty slot, so n = 10, p = 11
C(n, p) = n! / (n - p)! p!
C(n, p) = 10! / (10 - 11)! 11!
C(n, p) = 10! / (-1)! 11!
breaks again?

	

2 5 minute chunks to do exercises with
3 for cardio 3n
5 legs options 5n
4 choices for 
- chest, shoulders, back 4n ,4n, 4n,
triceps, 2 options 2n
back, 2 options 2n
abs 4 options 4n

