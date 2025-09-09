if you want the variable x to be 5, in python this is done with x = 5
	{=} means 'assign', or 'bind to'
		after this, executing 'x' would return 5 {if the previous or prior line states x = 5}
		running 'print(x)' outputs 5; given the above
		Python is case sensitive; $X \neq x$! 'print(X)' would return an error.

Can also assign multiple variables multiple integers; 'x,y = (1,2) will return '1 2' if instructed: print(x,y) or x,y
	NOTE* this also works for individual variables, so after running 'x,y = (1,2)', running print x or print y will return 1 & 2, respectfully

print("Click "OK"") is invalid
print('Click "OK"') is valid ^syntax

x = 10 {good}
x = [10] {will return [10] if print(x) is run, not 10}
	[] are used for lists of numbers 

in Python, there are Integers, Floats, and Boolean Values
	x1 = 5 {integer}
	[type(var)] = tells us the type of value the variable {x1} is
		type(x1) {returns 'int' for integer}
		x2 = 4.22 {then type(x2) returns 'float' for decimal}
				x1 = -5 and type(x1) would also return 'int' 

Reassigning Variables
x = 5
x {returns 5}
x = 1
x {returns 1; variable changed}
x + 1 {returns 6}

5 * 2 + 3 {equates the exact same as:}
5 * 2 + \
3

What if we wanted to extract 'd' from "Friday"?
"Friday" [3] {[] means indexing, so we specify the target for extraction in the bracket with the number of its position in Friday, so *starting at 0* F0 R1 I2 D3 A4 Y5, so 3