[S]tructured [Q]uery [L]anguage
SQL is designed specifically for relational database management
creates, manipulates, shares data through [ queries ]
	One can write and execute these queries through SQL

Most important language for data management in 2016, 2017

Why MySQL?
	SQL, NoSQL, Oracle, SQLite, Postscripts Sequel, etc.
	MySQL is reliable, mature, and open-source 
		used by Dropbox, Pinterest, Youtube, etc.,

[ DataBases ]
If the data is stored in rows and columns, it is in tabular form
	" purchase 1 was product 14 bought on Jan 1st, 2019, by customer 23 "
			this is one [ Record ] which is interchangeable with the word row
$$\begin{array} {|c|c|c|}
\hline
Purchase-Info\\
\hline
Purchase-ID & Date-of-Purchase & Customer-ID & Item-Code \\
\hline
1 & 1.1.2019 & 23 & 14 \\
2 & 2.6.2019 & 7 & 13 \\
3 & 3.7.2019 & 3 & 10 \\
\hline
\end{array}$$
$$\begin{array} {|c|c|c|}
\hline
Customer-Info\\
\hline
Customer-ID & Date-of-Join & Customer-Email & Last-Name \\ 
\hline
1 & 12.3.2018 & lopez@gmail.com & Lopez \\
2 & 2.1.2019 & louis@gmail.com & Louis \\
3 & 2.3.2019 & kicker@gmail.com & Kicker \\
\hline
\end{array}$$
We could stuff into one table, but would be inefficient ; they are better used in junction with one another than as a whole
	These databases are related through their customer ID's, which can be used to connect purchases to complains to specific items if another ' products ' table existed
		The smallest piece of data without modifying it is an entity
			A row of a table could be a row entity, and a column of a table could be a column entity