Database's tables need specifications of their values

Strings
	Strings are things like names or titles ; 'James', 'Jackson'
		These strings have a length of 5 and length of 7 respectively
	These strings both take up 5 bytes and 7 bytes, and take up 7 and 5 memory respectively
CHAR(5) 
	This sets the characters for the entries to be 5 characters, with a hard limit. 
		'James' would as well as 'Bob' but both would take up 5 bytes

VARCHAR(7)
	This sets another hard limit on character length but does adjust memory
		'James' would as well as 'Bob' but both would they would use 5 bytes and 3 bytes respectively

ENUM('M', 'F')
	This would restrict the input of the variable to either M or F, nothing more, nothing less, nothing else


Numerical Values
Integers 
Whole numbers, no decimal points
	TINYINT is between -128 and 128 and takes only 1 byte per entry
		If we chose unsigned integers, this, and any value, could only be positive
			In this case, TINYINT could be 0 - 255
	SMALLINT takes two bytes and is from -32,768 to 32,768
		It is 65,535 if unsigned
	And MEDIUMINT, UNT, BIGINT sizes 16,777,215, 4,294,967,295, & 18,446,744,073,709,551,615 respectively
		{ if unsigned ^, so divide by 2 if signing }

Fixed and Floating