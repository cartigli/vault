$$\begin{array} {|c|c|c|}
\hline
Sales\\
\hline
purchase-no & date-of-purchase & customer-id & item-code \\
\hline
1 & 1.1.2019 & 23 & 14 \\
2 & 2.6.2019 & 7 & 13 \\
3 & 3.7.2019 & 3 & 10 \\
\hline
\end{array}$$
For the table above, the values in date-of-purchase and item-code can be seen multiple times, as epexted

[ Primary Key ]
Purchase-No is unique, it will not repeat ever
	this is a Primary Key - single column
		unique identifiers of this table 
			they also cannot contain Null values at any point within a Primary Key

To make a relational schema, we make a rectangle with a title over the top, and 
	Always Underline the first value, which is always the Primary Key of this table$$\overset{\text{Sales}}{\begin{array} {|l|}
\hline
\underline{\text{purchase-no}}\\
\text{date-of-purchase} \\
\text{customer-id} \\
\text{item-code} \\
\hline
\end{array}} = \begin{array} {|c|c|c|}
\hline
Sales\\
\hline
purchase-no & date-of-purchase & customer-id & item-code \\
\hline
1 & 1.1.2019 & 23 & 14 \\
2 & 2.6.2019 & 7 & 13 \\
3 & 3.7.2019 & 3 & 10 \\
\hline
\end{array}$$
	This is a Relational Schema of the table Sales which possesses the Primary Key purchase-no and contains the data for date-of-purchase, customer, and the item-code$$\overset{\text{Sales}}{\begin{array} {|l|}
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
	The relational Schema above shows a table Sales which has the values Customer ID and Item Code, both of which correspond to the Customer ID and Items tables respectively. The item Customer ID of the Sales table points to information about the customer through the Customer ID like email, last name, and number of complains. In the same way, Item Code corresponds to another table of data containing unit cost, manufacturer, and company, of which company corresponds to yet another table containing information around this value. 
	The underlined value for every table is a Primary Key for that table. The items denoted with [fk] are foreign keys and correspond to a table containing additional information around the [fk] in which, they are the Primary Key. Foreign Keys don't denote anything within their own list and do not need to be unique.

[ Unique Keys ] are similar to Primary and Foreign keys but can contain Null values. An example is Contact No. Under Company's list, which cannot repeat because no two companies can have the same phone number, so they will be unique, but they can also be empty or Null without causing errors.
	
```tikz
\begin{document}
\begin{tikzpicture}
    % style neurons
    \tikzstyle{neuron}=[rectangle, draw, minimum size=14pt]
    
    % Define the four nodes
    \node[neuron] (Sales) at (0, 0) {Sales};
    \node[neuron] (Item) at (2, 1) {Item};
    \node[neuron] (CompanyID) at (4, 1) {Company ID};
    \node[neuron] (CustomerID) at (2, -1) {Customer ID};
    
    % Connect the nodes with lines
    % Sales connects to Customer ID and Item
    \draw (Sales) -- (CustomerID);
    \draw (Sales) -- (Item);
    
    % Item connects to Sales and Company ID
    \draw (Item) -- (CompanyID);
    % Note: Sales -- Item connection already drawn above
    
\end{tikzpicture}
\end{document}
```

Relationships between Tables
Despite the fact that Customer ID is a Primary Key for Customer ID list, meaning it never repeats and every value is unique and exists. However, the same information is seen in Sales with the Foreign Key value Customer ID. In Sales, the Customer ID value can repeat and likely will, as unique customers can make multiple purchases. This is a One to Many relationship. There is also Many to One, One to One, etc.,