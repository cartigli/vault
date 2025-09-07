cannot run {George} straight up
	'George' or "George" are fine, but both return 'George'
	print("George") and print('George') both return {George} without any quotations
Ex:
y = 10
print(y + " Dollars")
	however, we can modify these variables
	str() converts a number into test, so:
y = 10
str(y)
print(str(y) + " Dollars") {{doesn't throw an error}}

NOTE: modern solution is print(f"{y} Dollars")

'I'm fine' {wouldn't execute, error for invalid syntax}
"I'm fine" {would work, double quotes around single corrects}
'I\'m fine' {would also work}
	'\' is called an [Escape Character] and modifies the interpretation of the character directly after it

'Press "enter"' {outputs 'Press "enter"'}
"Press "enter"" {fails, returns error}

'Red' 'Car' {returns 'RedCar'}
'Red ' 'Car' {returns 'Red Car'}
print('Red ' + 'Car') {returns Red Car; quotations removed}
print('Red','Car') {returns Red Car; comma adds space between the words}

3, 5, 6.9, 7.0, 'car' {outputs (3, 5, 6.9, 7.0, 'car')}