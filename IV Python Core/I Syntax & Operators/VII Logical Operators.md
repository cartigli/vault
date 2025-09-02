Logical Operators: [Not, And, Or]  [[IV Python Core/I Syntax & Operators/VI Comparison Operators#^booleanOperators]]
	Boolean operators; return True or False 

And checks if the statements on either side are true
True and True {returns True}
True and False {returns False}
False and False {returns False}

Or checks whether
True or True {returns True}
True or False {returns True}
False or False {returns False}

Not leads to the opposite of the given f(x)
not True {returns False}
not False {returns True}

3>5 and 7>5
-> False
3>5 or 7>5
-> True
not 3>5
-> True
True or not True or not False
-> True
True and not True or not False
-> True

[The order of evaluation is 'not', then 'and', then 'or']
True and not True or not False {breaks down to...}
True and not True or True
True and False or True
True and True
True