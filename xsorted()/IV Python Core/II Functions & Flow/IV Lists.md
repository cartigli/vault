Lists are defined with a name and populated with Elements inside a bracket pair; [ ]

Disciples = ['John', 'Luke', 'Mathew', 'David']
Disciples {returns ['John', 'Luke', 'Mathew', 'David']}
	{can be any data type: [[IV Python Core/I Syntax & Operators/III Integers, Floats, and Boolean]]}

[ ] indicates the elements of a list/sequence
'' indicates the items composing of the list/sequence
	"list_name"[index_of_list] {returns the specified element}

[Indexing Lists]  [[xsorted()/IV Python Core/II Functions & Flow/VI Methods#^e2bf2b]]
Disciples[3] {would return 'David'}
	{accessed the list's value by 'indexing the value 3'}
Disciples[-1] {would return 'David'}
	Disciples[-2] {would return 'Mathew'}
		{{ negatives count from the last item {-1} to the left in descending order }}
		{{ positives start from 0 }}

[Replacing Objects in Lists] 
If we wanted to remove Mathew and replace him with Judas, we'd:
Disciples[-2] = 'Judas'
	then:
Disciples[2] {would return 'Judas'}

[Deleting Objects from Lists]
When the betrayal occurs, remove an item from the list with del list_name[index_value]
```python
del Disciples[2]
```
Disciples {would return ['John', 'Luke', 'David']}
	Now, Disciples[3] would return 'David'; the indexing schedule automatically updates

