[Slicing] takes specific items from a list; i.e., items 2-4 {[1:3]}

To get 'Luke' and 'John' from List = ['Thomas', 'Luke', 'John', 'Mary'];
	List[1:3] {returns 'Luke', 'John'}
	[1:] corresponds to the index of the first item of interest
	[:3] corresponds to the index of the last item of interest + 1

[Slicing{x:x}] ^slicing
List = ['Thomas', 'Mark', 'John', 'Mary']
List[1:3] {would return ['Mark', 'John']}

List[0:2] {returns ['Thomas', 'Mark']}
List[:2] {also returns ['Thomas', 'Mark']}

List[2:] {returns the index value of position 2 {3rd Element} to the last; ['John', 'Mary']}
List[3:] {returns the index of 3 {4th Element} to the last; ['Mary']}

List[-1] {returns the last Element of the list; 'Mary'}

List[-2:] {returns the 2nd to last Element, and the consecutive Elements until the last; ['John', 'Mary']}

Indexing can be used the reverse as well:
List.index('John') {returns the index value for that element in the list: 'List'; returns '2'}

Making a list of Lists
NewList = ['Josh', 'Alan']
BigList = [List, NewList]
BigList {returns [[ 'Thomas', 'Mark', 'John', 'Mary' ][ 'Josh', 'Alan' ]]} 
	{the two lists 'glued' together

[Methods for Modifying Lists]
see [[xsorted()/IV Python Core/II Functions & Flow/VI Methods]] for more details
	.sort(): organizes elements of a list
	.append(): adds an item to the end of a list
	.extend(): adds items from one list to the end of the specified list