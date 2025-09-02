in Python, there are Integers, Floats, and Boolean Values
	x1 = 5 {integer} [[xsorted()/IV Python Core/I Syntax & Operators/II Variables#^654d29]]
	[type(var)] = tells us the type of value the variable {x1} is
		type(x1) {returns 'int' for integer}
		x2 = 4.22 {then type(x2) returns 'float' for decimal}
				x1 = -5 and type(x1) would also return 'int'

[Integer()] ^integer
	if x2 = 4.33, and I run:
	int(x2)
		this would return 4 
		'int(var)' forces a variable into integer format
				{running float(x2) after int() will return the original value

[Float()] ^float
	float(var) transforms the variable into a floating value
		5 becomes 5.0
		4 becomes 4.0

[Boolean()] ^boolean
	True or False; 1's or 0's; On or Off
		'x3 = True' would return 'bool' if 'type(x3)' was run
				true and false, without capitol letters, would return errors as they are undefined, only True and False are Boolean values

[str()] ^string
	string value
	type(x) when x = 'boot' would return str
	[[xsorted()/IV Python Core/I Syntax & Operators/IV Strings]]

[type()] ^type
	tells you the type of variable specified
	type(5.0) {returns Float}
	type(5) {returns Int}
	type('cat') {returns str}