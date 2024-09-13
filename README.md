# SQL_Important_Links

### Most Important SQL Queries and Concepts

**Primary Key** is one of the candidate keys. One of the candidate keys is selected as the most important and becomes the primary key. There cannot be more than one primary key in a table.  

**Stored Procedures** are created to perform one or more DML operations on databases. It is nothing but a group of SQL statements that accepts some input in the form of parameters and performs some task and may or may not return a value.  

**BETWEEN:** The BETWEEN operator is used to fetch rows based on a range of values.  
For example,   

```sql
SELECT * FROM Students   
WHERE ROLL_NO BETWEEN 20 AND 30;  
```

**IN:** The IN operator is used to check for values contained in specific sets.  
For example, 

```sql
SELECT * FROM Students   
WHERE ROLL_NO IN (20,21,23);
```

This query will select all those rows from the table Students where the value of the field ROLL_NO is either 20 or 21 or 23.

