# SQL Theory

**1). Primary Key** is one of the candidate keys. One of the candidate keys is selected as the most important and becomes the primary key. There cannot be more than one primary key in a table.  

**2). Foreign key** is a field that can uniquely identify each row in another table. And this constraint is used to specify a field as a Foreign key.

**3). Stored Procedures** Stored Procedure is a function consists of many SQL statement to access the database system. Several SQL statements are consolidated into a stored procedure and execute them whenever and wherever required.

**4.1). BETWEEN:** The BETWEEN operator is used to fetch rows based on a range of values.  
For example,   

```sql
SELECT * FROM Students   
WHERE ROLL_NO BETWEEN 20 AND 30;  
```

**4.2). IN:** The IN operator is used to check for values contained in specific sets.  
For example, 

```sql
SELECT * FROM Students   
WHERE ROLL_NO IN (20,21,23);
```

This query will select all those rows from the table Students where the value of the field ROLL_NO is either 20 or 21 or 23.

**5). JOIN** statement is used to combine data or rows from two or more tables based on a common field between them.

**6.1). Index :** A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and the use of more storage space to maintain the extra copy of data. 

**6.2). Indexing :** Indexing makes columns faster to query by creating pointers to where data is stored within a database.  
[Indexing](https://www.atlassian.com/data/sql/how-indexing-works)

**7). Trigger :** is a statement that a system executes automatically when there is any modification to the database. In a trigger, we first specify when the trigger is to be executed and then the action to be performed when the trigger executes.

**8). Cluster and Non-Cluster Index :**
| Clustered Index | Non-Clustered Index |
|----------|----------|
| The clustered index is faster.    | The non-clustered index is slower. |
| The clustered index requires less memory for operations.    | The non-Clustered index requires more memory for operations.   | 
| A table can have only one clustered index.    | A table can have multiple non-clustered indexes. |
| In the Clustered index, the Clustered key defines the order of data within the table.    | In the Non-Clustered index, the index key defines the order of data within the index.   | 
| In a clustered index, the index is the main data.    | In the Non-Clustered index, the index is a copy of data. |

[What is the difference between Clustered and Non-Clustered Indexes in SQL Server?](https://www.sqlshack.com/what-is-the-difference-between-clustered-and-non-clustered-indexes-in-sql-server/)

**9). DROP and TRUNCATE statements :**
| DROP | TRUNCATE |
|----------|----------|
| The DROP command is used to remove the table definition and its contents.    | Whereas the TRUNCATE command is used to delete all the rows from the table. |
| In the DROP command, table space is freed from memory.    | While the TRUNCATE command does not free the table space from memory.   | 
| In the DROP command, a view of the table does not exist.    | While in this command, a view of the table exists. |
| The DROP command is quick to perform but gives rise to complications.    | While this command is faster than DROP.   | 

**10). How do we avoid getting duplicate entries in a query without using the distinct keyword?**  
DISTINCT is useful in certain circumstances, but it has drawbacks that it can increase the load on the query engine to perform the sort (since it needs to compare the result set to itself to remove duplicates). We can remove duplicate entries using the following options:
- Remove duplicates using row numbers.
- Remove duplicates using self-Join.
- Remove duplicates using group by.

**11). What is the difference between COALESCE() & ISNULL()?**  
- **COALESCE():** COALESCE function in SQL returns the first non-NULL expression among its arguments. If all the expressions evaluate to null, then the COALESCE function will return null.
Syntax:
```sql
SELECT column(s), CAOLESCE(expression_1,….,expression_n)FROM table_name;
```

- **ISNULL():** The ISNULL function has different uses in SQL Server and MySQL. In SQL Server, ISNULL() function is used to replace NULL values.
Syntax:
```sql
SELECT column(s), ISNULL(column_name, value_to_replace)FROM table_name;
```

# SQL query

**1). SQL query to find the names of employees starting with ‘A’.**

```sql
SELECT * FROM Employees WHERE EmpName like 'A%' ;
```

**2). How can you create an empty table from an existing table?**

```sql
Select * into studentcopy from student where 1=2
```
