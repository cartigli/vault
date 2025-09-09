Another way to sort data is Dictionaries
	dictionaries contain keys paired to an associated value
	they are defined with {} and [Key-Value Pairs]

dict ={'w1': "cat", 'w2': "dog", 'w3': "fish", 'w4': "person"}
	this example has four keys; {w2: dog} is a [Key-Value Pair] ^keyvalue

a value can be assessed by its key rather than its index
dict['w2'] {returns 'dog'}
	dict[w2] {throws an error}

instead of .append() or .extend(), we add to dictionaries by defining the new [Key-Value Pair]
dict['w5'] = "koifish" {could be single quotes}
dict {would return {'w1': "cat", 'w2': "dog", 'w3': "fish", 'w4': "person", 'w5': "koifish"}

Alter a [Key-Value Pair] the same way:
dict['w2']='ratdog' {would replace 'dog' with 'ratdog' for the w2 Key-Pair}

If one person works in room1, and 3 in room2, how would we define in a dictionary?
dict={'room1': 'Jennifer', 'room2': ['Jack', 'John', 'Jane']}
dict['room2'] {would output ['Jack', 'John', 'Jane']}

Another way to populate a dictionary:
team={}
team['right bench']='joe'
team['left bench']='jack'
team['center bench']='jane'
team['stayed home']='jill'
team
-> {'right bench': 'joe', 'left bench': 'jack', 'center bench': 'jane', 'stayed home': 'jill'}
print(team)
-> {'right bench': 'joe', 'left bench': 'jack', 'center bench': 'jane', 'stayed home': 'jill'}
print(team['stayed home'])
-> jill

[.get()] ^get
'gentler' than print/or naming, if exists, will return the value, if doesn't, returns 'None'
print(team.get('stayed home')) {returns "jill"}
print(team.get('bench-warmer')) {returns 'None'} ^ad4081

team
-> {'right bench': 'joe', 'left bench': 'jack', 'center bench': 'jane', 'stayed home': 'jill'}
coaches=['mrm', 'mrt', 'mrsb']
team['coaches']=(coaches)
team
-> {'right bench': 'joe', 'left bench': 'jack', 'center bench': 'jane', 'stayed home': 'jill', 'coaches': ['mrm', 'mrt', 'mrsb']}