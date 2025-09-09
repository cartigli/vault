Methods of Modifying Lists

object: Parameters = [ 'ok', 'yes', 'no' ]
dot operator: '.': invokes a command
-append() : method
	{{ methods use dot notation; functions do not }}

[ .append() ]
Parameters.append('maybe')
	Parameters {is now ['ok', 'yes', 'no', 'maybe']} ^eb39eb

[ .extend() ]
Same could be accomplished through the .extend( ) method
Parameters.extend(['Hell yeah'])
Parameters {is now [ 'ok', 'yes', 'no', 'maybe', 'Hell yeah' ]}
	.extend() requires the brackets & the quotations: ''
	it 'extends' the list of Parameters by the list defined in .extend([' '])
	print('The first parameter is ' + Parameter[0] + '.') {no quotations around the Parameters[0] indexing}

[ .index() ]
object.index('Element-Argument') outputs the index value of the Element entered as an argument in regards to the list: 'object' ^e2bf2b
	start at 0, negatives {{ from -1 }} start at the end

[ .sort() ]
.sort() method organizes elements of a list
	default is alphabetical/numerical order
	list=[1,2,3,4]
	list.sort(reverse=True)
	list
	>4,3,2,1
	>list.sort()
	>list
	>1,2,3,4

command(argument) is not the same as object.operation(argument)