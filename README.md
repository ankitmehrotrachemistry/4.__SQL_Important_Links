# SQL_Important_Links

### Most Important SQL Queries and Concepts

**1). Primary Key** is one of the candidate keys. One of the candidate keys is selected as the most important and becomes the primary key. There cannot be more than one primary key in a table.  

**2). Foreign key** is a field that can uniquely identify each row in another table. And this constraint is used to specify a field as a Foreign key.

**3). Stored Procedures** are created to perform one or more DML operations on databases. It is nothing but a group of SQL statements that accepts some input in the form of parameters and performs some task and may or may not return a value.  

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

**SQL query to find the names of employees starting with ‘A’.**

```sql
SELECT * FROM Employees WHERE EmpName like 'A%' ;
```
**6). Index :** A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and the use of more storage space to maintain the extra copy of data. 

**7). Trigger :** is a statement that a system executes automatically when there is any modification to the database. In a trigger, we first specify when the trigger is to be executed and then the action to be performed when the trigger executes.

**8). Cluster and Non-Cluster Index :**
| Clustered Index | Non-Clustered Index |
|----------|----------|
| The clustered index is faster.    | The non-clustered index is slower. |
| The clustered index requires less memory for operations.    | The non-Clustered index requires more memory for operations.   | 
| A table can have only one clustered index.    | A table can have multiple non-clustered indexes. |
| In the Clustered index, the Clustered key defines the order of data within the table.    | In the Non-Clustered index, the index key defines the order of data within the index.   | 
| In a clustered index, the index is the main data.    | In the Non-Clustered index, the index is a copy of data. |

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
