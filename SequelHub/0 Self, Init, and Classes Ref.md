I want to get more complex and scale, so I am introducing these fundamentals for more robust Python scripts.

[ Class ] 
A blueprint for creating objects; a template for defining the State {attributes/data} and Behavior {methods/functions}.

`__init__`: a Python constructor - initializes new instances of a class automatically when new objects are created
	Keep it simple: no heavy computations or expensive I/O operations
	Have default parameters for optional attributes
	Validate earlier rather than later

```python
class BankAccount:
	def __init__(self, account_holder, initial_balance=0):
		# instance attributes are unique to each object
		self.holder = account_holder
		self.balance = initial_balance
		self.transaction_history = []

		# log it
		self.transaction_history.append(
			f"Account created with balance: ${initial_balance}")
```

`self`: a reference to the current instance of the class; how an object accesses its own attributes and methods
		<u>Python automatically passes self as the first parameter to all instance methods</u>

```python
class Student:
	def __init__(self, name, student_id):
		self.name = name # self.name belongs specifically to THIS student
		self.student_id = student_id
		self.grades = []

	def add_grade(self, grade):
		# self allows us to modify THIS student's grades
		self.grades.append(grade)

	def calculate_gpa(self):
		# and self let's us access THIS student's data
		if not self.grades:
			return 0.0
		return sum(self.grades)/len(self.grades)
```

__ init __ is kind of like the set up process that runs whenever a new, unique object is creates from the class blueprint.
It sets them up with the layout defined in the blueprint; the attributes and state are defined and given to the object.
	There are also Class Variables, which are shared across instances of a class; species in the Python below is defined at the Class level above or outside of __ init __ .
```python
class Dog:
	# class variable shared by all dog instances
	species = "Canis familiaris"

	def __init__(self, name, age):
		# instance variables ; unique to each dog instance
		self.name = name
		self.age = age
		self.tricks = []

# creating two dog objects { instances }
dog_1 = Dog("Buddy", 3)
dog_2 = Dog("Lucy", 5)

print(f"{dog_1.name} is a {dog_1.species}.") # Buddy is a Canis familiaris
print(f"{dog_2.name} is a {dog_2.species}.") # Buddy is also a Canis familiaris
```

Self connects an object's attributes to its methods; when we call a method on an object, python automatically passes that object into the method as the first argument; self. In this way, a method can modify or read the attributes of the specific instance being passed.

```python
class Dog:
	# class variable shared by all dog instances
	species = "Canis familiaris"

	def __init__(self, name, age):
		# instance variables ; unique to each dog instance
		self.name = name
		self.age = age
		self.tricks = []

	# ' self ' refers to the specific dog object the method is called on
	def add_trick(self, trick):
		print(f"{self.name} is learning a new trick: {trick}!")
		self.tricks.append(trick) # modify THIS dog's list of tricks

	# & self gives access to other instance's data or attributes
	def bark(self):
		print(f"{self.name} says Woof!")

# create an instance
my_dog = Dog("Rex", 4)

# when you call my_dog.add_trick("roll over"), Python internally does the following:
#   Dog.add_trick(my_dog, "roll over")
my_dog.add_trick("roll over")

# self assures we are accessing the attributes of my_dog
print(my_dog.tricks) # outputs ['roll over']
```