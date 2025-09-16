MySQL uses relational databases, while non-relational databases are more complex 

Main Goal is to organize and make easily receivable databases for large amount of data
	Bigger the database or table, the slower the response
		It is faster to have multiple, separate collections which can be used in junction with one another
	Theory related to relational algebra 

Consider Venn diagrams; circle a could be something and circle b could be another, while they have small overlap
	If we have one massive circle, looking through this would be difficult and tedious
		Splitting into multiple circles for combining like terms and common fields makes extracting data much easier
			Saves energy == more efficiency
				This makes a Relational Database Management System, or [ RDMS ]

[ Spreadsheet ] 
An electronic ledger
	It is possible to make tables within them
	Both can make large amount of data 
	Can implement equations and calculations
	Every cell is treated as an individual entity
	Can apply formatting to all cells
		This is more formatted and properly set to some value

[ Database ]
Databases have no definitions for their contents
	Contain raw data, every cell contains some value
	The type of data contained in a certain data must be preset
		Ex: field of date columns, user tries to insert a string, an error is returned
			In excel, this would be fine
		There is also no formatting, and 
		Size of data is found by the length, in excel, the length is $\infty$
			No calculations are computed or equations implemented

If you needed a database for your business, you wouldn't hire a data analysis, you'd hire a database designer 
	They will be in charge of configuring the tables as well as the relationship between them
		A way they do this is by plotting the entire database's structure and relationships
			One of two methods for this is the Entity Relationship Diagram [ ER ]
				Like a flow chart of the relationship between tables and data
			Another is the Relational Schema { shown below, tables are connected via references of more tables
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