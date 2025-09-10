The SQL tool that allows us to construct a relationship between objects.

Joins must be constructed over a column the two tables have in common. It shows a result set, containing fields *derived* from two or more tables.

```
  ┌────────────────┐           ┌──────────────────┐      ┌────────────────────┐
  │  employees     │─||──────|<┤  dept_manager    │>|─── ┤   departments      │
  ├────────────────┤           ├──────────────────┤      ├────────────────────┤
  │PK mep_no INT   │           │FK dept_no CHAR4  │  ┌─││┤PK dept_no CHR4     │
  │ birth_date DATE│─||─────┐  │FK emp_no INT     │  │   │   dept_name VCHR40 │
  │ first_name VCHR│        │  │   from_date DATE │  │   └────────────────────┘
  │ last_name VCHR │─||───┐ │  │   to_date DATE   │  │   ┌──────────────────┐
  │  gender ENUM   │      │ │  └──────────────────┘  └─|<┤   dept_emp       │
  │ hire_date DATE │─||─┐ │ └──────────────────────────|<┼──────────────────┤
  └────────────────┘    │ │     ┌─────────────────────┐  │FK emp_no INT     │
     ┌──────────────────┘ └───|<┤     titles          │  │FK dept_no CHR4   │
     │    ┌──────────────────┐  ├─────────────────────┤  │   from_date DATE │
     └──|<┤    salaries      │  │ FK emp_no INT       │  │   to_date DATE   │
          ├──────────────────┤  │    title VARCHAR(50)│  └──────────────────┘
          │ FK emp_no INT    │  │    from_date DATE   │
          │    salary INT    │  │    to_date DATE     │
          │    from_date DATE│  └─────────────────────┘
          │    to_date DATE  │
		  └──────────────────┘
```


INNER JOIN
Below we have both out tables Dept_manager  and Departments shown as circles. Together, they have the dept_no in common,; as an item of the table Dept_manager, and as the Primary Key of the Departments table. Therefore, the Result Set of these two tables is dept_no.

```tikz
\begin{document}
\begin{tikzpicture}
    % Three overlapping circles
    \draw (-1,0) circle (2.2cm);
    \draw (1,0) circle (2.2cm);
    
    % Add labels at top
    \node at (1.75,2.5) {\textbf{Departments}};
    \node at (-1.75,2.5) {\textbf{Dept-manager}};
    
    % Rectangle in the overlap
    \node[align=left, font=\small] at (0,.5) {
        dept\_no
    };
    
    % List in Departments circle (left)
    \node[align=left, font=\small] at (2.2,0) {
        dept\_no\\
        dept\_name
    };
    
    % List in Dept-manager circle (right)  
    \node[align=left, font=\small] at (-2.2,0) {
        dept\_no\\
        emp\_no\\
        from\_date\\
        to\_date
    };
\end{tikzpicture}
\end{document}
```
*Dept_no is the matching value here, and the rest are considered non-matching records in this case.*

```mysql
SELECT 
	table_1.column_name[s], table_2.column_name[s]
FROM 
	table_1
JOIN 
	table_2 ON table_1.column_name = table_2.column_name;
```
*1. Select all columns you wish to see in the result and the tables they originate from. 2. FROM and JOIN show the tables we are matching. 3 ON relates the columns by quoting them over the equals sign to show SQL where to pull the matching values from.*

*You can also give an alias for the table names without the AS command in this case:*
```mysql
SELECT 
	t1.column_name[s], t2.column_name[s],
FROM 
	table_1 t1
JOIN 
	table_2 t2 ON t1.column_name = t2.column_name;
```
*This way it becomes much easier to spell out the entire relationship.*

Practice with the preconfigured dataset: Retrieve all employee numbers (`emp_no`) and contract start dates (`from_date`) from the department employees table (`dept_emp`). Add a third column, displaying the name of the department they have signed for (`dept_name` from the `departments`table):
```mysql
SELECT 
	de.emp_no, de.from_date, d.dept_name
FROM 
	dept_emp de
INNER JOIN 
	departments d ON de.dept_no = d.dept_no
ORDER BY 
	de.emp_no;
```
*We are making a Inner Join of the two given tables over their common ground; dept_no. We specified the join we would like to complete and then defined the connection over which the join should be made. We also defined their aliases with From and Inner Join. The columns they are joined over need not be named the same.*
	*In our practice set, the departments table had some Null values in both columns of its contents. Neither of either of these values are considered as only Non-Null matching values are in play. If there is a complete record in one table that is vacant in the other, it will not be shown*
			*If the result set is empty, this simply means their are no relationships between the tables.*

LEFT JOIN
A join of the components of the primary table in the join.
	*It is akin to all the matching values of two tables plus all the values of the primary table that match no values from the secondary values.*
