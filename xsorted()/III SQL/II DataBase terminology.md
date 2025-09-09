MySQL uses relational databases, while non-relational databases are more complex 

main goal: organize and make easily receivable databases for large amount fo data
	bigger the database or table, the slower the response
		it is faster to have multiple, separate collections which can be used in junction with one another
	theory related to relational algebra 

consider Venn diagrams, circle a could be something and circle b could be another, while they have small overlap
	if we have one massive circle, looking through this would be difficult and tedious
		splitting into multiple circles for combining like terms and common fields makes extracting data much easier
			saves energy == more efficiency
				this makes a Relational Database Management System, or [ RDMS ]

dif between a database and a spreadsheet
Spreadsheet: an electronic ledger
	it is possible to make tables within them
	both can make large amount of data 
	can implement equations and calculations
	every cell is treated as an individual entity
	can apply formatting to all cells
		this is more formatted and properly set to some value

Database :
	Databases have no definitions for their contents
	contain raw data, every cell contains some value
	the type of data contained in a certain data must be preset
		ex: field of date columns, user tries to insert a string, an error is returned
			in excel, this would be fine
		there is also no formatting, and 
		size of data is found by the length, in excel, the length is $\infty$
			no calculations are computed or equations implemented

if you needed a database for your business, you wouldn't hire a data analysis, you'd hire a database designer 
	they will be in charge of configuring the tables as well as the relationship between them
		a way they do this is by plotting the entire database's structure and relationships
			one of two methods for this is the Entity Relationship Diagram [ ER ]
				like a flow chart of the relationship between tables and data
			another is the Relational Schema { shown below, tables are connected via references of more tables
$$\overset{\text{Sales}}{\begin{array} {|l|}
\hline
\underline{\text{Purchase No. [pk]}}\\
\text{Date of Purchase} \\
\text{Customer ID [fk]} \\
\text{Item Code [fk]} \\
\hline
\end{array}} , \overset{\text{Customer ID}}{\begin{array} {|l|}
\hline
\underline{\text{Customer ID [pk]}}\\
\text{Last Name} \\
\text{Email} \\
\text{No. Complaints} \\
\hline
\end{array}},\overset{\text{Items}}{\begin{array} {|l|}
\hline
\underline{\text{Item Code [pk]}}\\
\text{Item} \\
\text{Unit Cost} \\
\text{Company ID [fk]} \\
\hline
\end{array}}, \overset{\text{Company}}{\begin{array} {|l|}
\hline
\underline{\text{Company ID [pk]}}\\
\text{Company} \\
\text{Contact No.} \\
\text{No. of Products} \\
\hline \end{array}}$$