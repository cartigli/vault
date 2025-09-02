How do we iterate through values or Elements of a [Dictionary]? How much did we spend at the grocery?
```python
prices = {}
"box_of_spaghetti": 4
"lasagna": 5
"hamburger": 2

quantity = {
	"box_of_spaghetti": 6,
	"lasagna": 10,
	"hamburger": 0
}
```
to answer the question, quantities must be multiplied by price
	the quantities and price of one item are connected to the same Key-Values
```python
money_spent = 0

for i in prices:
	money_spent = money_spent + (quantity[i] * price[i])
print(money_spent)
```
{{ 74 }}

**adding ['pasta']=15 to quantity and NOT to prices resulted in 148; not 74 or a error message. How exactly does a loop like this work? What limitations or special cases should I know about with this design for future coding?**

ANSWER: adding a variable to quantity didn't break the loop because the loop was directed to prices. Adding a variable to prices, or changing prices to quantity, would both break the loop. Furthermore, the additional variable caused an additional loop which ran the previous calculations twice; 74 + 74 = 148
	{{ adding money_spent = 0 after the 'for i in prices:' line repaired the miscalculation, but does not repair the issue caused when switching between ...i in prices... and ...i in quantity... }}