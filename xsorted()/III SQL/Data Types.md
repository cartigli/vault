Database's tables need specifications of their values

[ Numeric ]

[ Integers ]
Whole numbers, no decimal points

TINYINT is between -128 and 128 and takes only 1 byte per entry
	If we chose unsigned integers, this, and any value, could only be positive
		In this case, TINYINT could be 0 - 255
SMALLINT takes two bytes and is from -32,768 to 32,768
	It is 65,535 if unsigned
MEDIUMINT, UNT, BIGINT are sizes 16,777,215, 4,294,967,295, & 18,446,744,073,709,551,615 respectively
		{ if unsigned ^, so divide by 2 and spread over 0 if signing }

[ Fixed ]
Precision is a term for the digits in the variable ; 10.523 is precision 5
Scale refers to the number of digits to the right of the decimal ; 10.523 is scale 3

DECIMAL( p, s ) where p is precision and scale
	DECIMAL( 5, 2 )
		DECIMAL( 12345) would be 123.45
			DECIMAL( 123) would be 123.00
				DECIMAL( 123456) would be 123.46 { rounded up }
	NUMERIC has the same notation and function for ( precision, scale )

[ Floating ]
Approximates values and aims to balance between range & precision

FLOAT( 5, 3 ) would work for 10.523 and round 10.5235
	FLOAT is 4 bytes for a maximum of 23 digits | single precision
DOUBLE( ) works the same but is twice the size in bytes
	DOUBLE is 8 bytes for a maximum of 53 digits | double precision


[ Strings ]
Must be written with quotes 
Alphanumeric values containing strings of letters
	'James' is a string with length of 5 symbols, and so takes 5 bytes of storage
	
CHAR(5) 
	This sets the characters for the entries to be 5 characters, with a hard limit. 
		'James' would as well as 'Bob' but both would take up 5 bytes
			maximum character in any string is 255 but faster than VARCHAR
VARCHAR(7)
	This sets another hard limit on character length but does adjust memory
		'James' would as well as 'Bob' but both would they would use 5 bytes and 3 bytes respectively
			maximum character in any string is 65.535
ENUM('M', 'F')
	This would restrict the input of the variable to either M or F, nothing more, nothing less, nothing else

[ Other Data Types ]

DATE
	Dates range from 1st of January, 1000 to 31st of December, 9999
		Stored in the format YYYY-MM-DD
		September 7th, 2025 would be ' 2025-09-07 '

DATETIME
	YYYY-MM-DD HH:MM:SS[.fraction]
		3:22 on the same day would be ' 2025-09-07 15:27:41.52 ' or whatever desired precision
			ranges from 00:00:00.0 to 23:59:59.999999

TIMESTAMP
	This is a well defined and more exact point in time than DATETIME
		It records the moment in time as the number of seconds passed after the 1st of January 1970 00:00:00 UTC
			1757361550 was the current UTC at the time of me writing this
				It had been 1,757,361,550 seconds since January 1st, 1970 00:00:00
			UTC = Coordinated Universal Time
			Appropriate over time-zones while DATETIME is not ; TIMESTAMP does not consider time zones when counting seconds

BLOB
Binary Large Object
	Refers to a considerably sized series of 1's and 0's that contain information for a file like .xml, .doc, .wav, etc.,