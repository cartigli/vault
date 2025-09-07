We have a Database of user's purchase history from an audiobook application's information

Every customer in the database has bought at least once and we need to determine their likelihood of purchasing again
	this way, the company can target advertisements to those liekely to purchase again
		it will find the important metrics that determine a customer's likelihood of purchasing again

Dataset:
	every row is a person
		columns:
			customer id
			book length - sum of all books bought by customer
			average book length - sum divided by num of purchases
			price overall - sum of all
			price average - divided by number of purchases
			review - boolean whether or not they reviewed
			review /10 - if they left a review, its score out of ten
				{ preprocessing } since most users did not leave a review, we can fill these non-entries with the average customer review, making reviews above it and below it more meaningful while enabling the non-review customers to be included in the analysis
			Minutes Listened
			Completion - total minutes listened divided by total of books purchased
			support requests - count of support requests opened by a customer , forgot password, download issues, etc.,
			Last Visit - Purchase Date - time between engagements
	Targets: 0's or 1's
		we collected data over 2 years, and then found the following 6 months of the same customer's habits, and determined if they made another purchase