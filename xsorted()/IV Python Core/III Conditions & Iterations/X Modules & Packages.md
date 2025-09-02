Module: pre-written code containing definitions of variables, functions, and classes
Package: a collection or directory of relates Python modules {{ Aka: a Library }}

Python's Standard Library:
	available as soon as you isntall python
		.len() is a python package
		also, use methods from list class to list items from an object
				neither required defining in our script

How to use a Library:
	four ways to do so:
task: import 'math' module; functions like sqrt() or log()
```python
import math
math.sqrt(16)
```
or
```python
from math import sqrt
sqrt(16)
```
or
```python
from math import sqrt as s
s(16)
```
or
```python
import math as m
m.sqrt(9)
```
or least efficiently
```python
from math import *
sqrt(9)
```
could have function or formula confusion if done with multiple Libraries; specificity is better and more professional in code
```python
from math import sqrt
help(math) # shows more info on functions and methods of the Library specified
help(math.sqrt) # can show more specific information of a Library's function and its uses
```